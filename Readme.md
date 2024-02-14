# Increase EBS Volume Size in AWS

## Steps to Increase EBS Volume Size

### Step 1: Take Snapshot of EBS Volume (to be Safe).

Take a snapshot of the EBS volume in AWS to ensure you have a backup before making changes.

### Step 2: Increase EBS Volume Size in AWS Console.

Go to the AWS Console and modify the EBS volume to the desired new size.

### Step 3: Extend a Linux file system after resizing a volume.

Once the volume size is increased, extend the Linux file system to make use of the new volume size.

## Commands to Extend the File System

First, check the file system usage:

```
df -hT
```

Check whether the volume has a partition:

```
sudo lsblk
```

### Extend the Partition:

To extend the partition, use the `growpart` tool:

```
sudo growpart /dev/xvda 1
```

After growing the partition, check the block devices again:

```
sudo lsblk
```

Check file system usage once more:

```
df -hT
```

### Extend the File System on `/`

Depending on your file system type, use one of the following commands:

For XFS file system:

```
sudo xfs_growfs -d /
```

For Ext4 file system:

```
sudo resize2fs /dev/xvda1
```
### For checking file size
```
sudo find / -type f -size +10M -exec ls -lh {} \;
```
After completing these steps, your EBS volume's file system will be extended to utilize the full capacity of the increased volume size.
