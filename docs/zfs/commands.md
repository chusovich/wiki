# ZFS Commands

## Pools and vDevs

### Create a mirror pool
create a new pool called new-pool using the devices /dev/sdb and /dev/sdc in a mirror
```terminal
sudo zpool create new-pool mirror /dev/sdb /dev/sdc
```
You can also use the ```-m``` option to specify the mount point. The default mount point is ```/poolname```
```console
sudo zpool create -m /usr/sharepool new-pool mirror /dev/sdb /dev/sdc
```

### Checking the status of all zfs pools
```bash
sudo zpool status
```

### Add devices to an existing ZFS pool
add the devices /dev/sdb and /dev/sdc to the pool called existing-pool 
```yaml
zpool add existing-pool mirror /dev/sdb /dev/sdc
```

## Datasets

#### Create a new dataset
Create a dataset named 'mydataset' on the pool 'mypool'
```rust
sudo zfs create mypool/mydataset
``` 

#### Check the dataset seize
```go
sudo zfs list mypool/dataset
```

#### Set additional properties
```cpp
sudo zfs set compression=on mypool/mydataset # turns on compression
sudo zfs set quota=10G mypool/mydataset # set the sixe quota to 10GB
sudo zfs get quota /mypool/mydataset # view the quota of the dataset
```
