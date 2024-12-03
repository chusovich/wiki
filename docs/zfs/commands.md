# ZFS Commands

## Pools and vDevs

``` title="Create a mirrored pool"
# create a new pool called new-pool using the devices /dev/sdb and /dev/sdc in a mirror
sudo zpool create new-pool mirror /dev/sdb /dev/sdc
# you can also use the -m option to specify the mount point
# the default mount point is /poolname
sudo zpool create -m /usr/sharepool new-pool mirror /dev/sdb /dev/sdc
```

### Checking the status of all zfs pools
```
sudo zpool status
```

``` title="Adding devices to an existing ZFS pool"
# add the devices /dev/sdb and /dev/sdc to the pool called existing-pool 
zpool add existing-pool mirror /dev/sdb /dev/sdc
```

## Datasets
``` title="Create a dataset named 'mydataset' on the pool 'mypool'"
sudo zfs create mypool/mydataset
``` 

```title="Check the dataset size"
sudo zfs list mypool/dataset
```

``` title="Set additional properties"
sudo zfs set compression=on mypool/mydataset # turns on compression
sudo zfs set quota=10G mypool/mydataset # set the sixe quota to 10GB
sudo zfs get quota /mypool/mydataset # view the quota of the dataset
```
