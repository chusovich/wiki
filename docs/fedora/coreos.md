## CoreOS

## 
- install coreOS
- create ignition file

```
variant: fcos
version: 1.6.0
passwd:
  users:
    - name: core
      ssh_authorized_keys:
        - ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIFbrRHrIg/vbvotrutNkzpx/JusupdM4XfozS14vqlir baldrick
      groups:
        - wheel
        - sudo
        - docker

storage:
  files:
    - path: /etc/hostname
      mode: 0644
      contents:
        inline: derp
    - path: /etc/zincati/config.d/90-disable-auto-updates.toml
      mode: 0644
      contents:
        inline: |
          [updates]
          enabled = false
    - path: /etc/systemd/system/rpm-ostree-countme.timer.d/40-weekly.conf
      mode: 0644
      contents:
        inline: |
          [Timer]
          OnCalendar=weekly
    - path: /etc/modules-load.d/zfs.conf
      mode: 0644
      contents:
        inline: zfs

systemd:
  units:
    - name: rpm-ostree-rebase-to-ucore.service
      enabled: true
      contents: |
        [Unit]
        Description=Rebase to uCore
        Wants=network-online.target
        After=network-online.target
        Before=zincati.service
        ConditionPathExists=!/var/lib/rpm-ostree-rebase-to-ucore.stamp

        [Service]
        Type=oneshot
        RemainAfterExit=yes
        ExecStart=/usr/bin/rpm-ostree rebase --reboot ostree-unverified-registry:ghcr.io/ublue-os/ucore-minimal:stable-zfs
        ExecStart=/usr/bin/touch /var/lib/rpm-ostree-rebase-to-ucore.stamp

        [Install]
        WantedBy=multi-user.target
        
    - name: docker.socket
      enabled: true
      contents: |
        [Unit]
        Description=Docker Socket for the API
        PartOf=docker.service

        [Socket]
        ListenStream=/var/run/docker.sock
        SocketMode=0660
        SocketUser=root
        SocketGroup=docker

        [Install]
        WantedBy=sockets.target
    - name: zfs-load.service
      enabled: true
      contents: |
        [Unit]
        Description=Load ZFS kernel module
        DefaultDependencies=false
        After=systemd-modules-load.service
        Before=zfs-mount.service

        [Service]
        Type=oneshot
        RemainAfterExit=yes
        ExecStart=/usr/sbin/modprobe zfs

        [Install]
        WantedBy=sysinit.target
```
