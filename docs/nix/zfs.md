# ZFS on NixOS

## Example Configuration Settings
```nix
# Networking
networking.hostId = "4f98920a"; # this is used to make sure the pool is imported on the correct machine

# ZFS
boot.supportedFilesystems = [ "zfs" ]; # enable zfs
boot.zfs.forceImportRoot = false; # this option forces the import of zfs root pools, which we don't care about or wnat
boot.zfs.extraPools = [ "my-pool" "my-other-pool" ]; # mount the pools listed on boot
services.zfs.autoScrub = {
  enable = true; # enable autoscrubbing
  interval = monthly; # default interval for autoscrub is every month
};
services.zfs.autoSnapshot = {
  enable = true; # enable snapshots
  montly = 12; # number of monthly snapshots to keep
  weekly = 52; # number of weekly snapshots to keep
  daily = 7; # dido
  hourly = 24; # dido
  frequent = 4; # number of 15 min interval snapshots to keep
};  
```
