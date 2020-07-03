# VMware 磁盘碎片空间回收

> ## 提示
> 需要将快照删除

## Ubuntu或者Centos

### 第一步：将碎片空间填充上0

```
sudo dd if=/dev/zero of=/0bits bs=20M
```

### 第二步：删除第一步的填充

```
sudo rm /0bits
```

### 第三步：关闭虚拟机，打开windows命令行工具cmd，用cd命令进入WMware的安装文件夹，如cd C:\Program Files (x86)\VMware\VMware Workstation。该目录下有个vmware-vdiskmanager为VMware自带的磁盘空间回收工具，执行vmware-vdiskmanager.exe -k "虚拟机文件目录\虚拟机名称.vmdk"。

```
C:\Program Files (x86)\VMware\VMware Workstation\vmware-vdiskmanager.exe -k "C:\Centos\Centos7.vmdk"
```

执行过程中会显示进度，完成后会提示：
Shrink:100% done.
shriink completed successfully.


