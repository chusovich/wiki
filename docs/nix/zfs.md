# ZFS on NixOS
see the [NixOS Wiki](https://nixos.wiki/wiki/ZFS#Declarative_mounting_of_ZFS_datasets) on ZFS, or look up specific options using the [NixOS options search](https://search.nixos.org/options?)

## Example Configuration Settings
```nix
# Networking
networking.hostId = "4f98920a"; # used to make sure the pool is imported correctly

# Basic ZFS Settings
boot.supportedFilesystems = [ "zfs" ]; # enable zfs
boot.zfs.forceImportRoot = false; # force the import of zfs root pools
boot.zfs.extraPools = [ "my-pool" "my-other-pool" ]; # mount the pools listed on boot

# Autoscrubbing settings
services.zfs.autoScrub = {
  enable = true; # enable autoscrubbing
  interval = monthly; # default interval for autoscrub is every month
};

# Autosnapshot settings
services.zfs.autoSnapshot = {
  enable = true; # enable snapshots
  montly = 12; # number of monthly snapshots to keep
  weekly = 52; # number of weekly snapshots to keep
  daily = 7; # dido
  hourly = 24; # dido
  frequent = 4; # number of 15 min interval snapshots to keep
};  
```
