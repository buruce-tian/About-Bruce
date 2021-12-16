# IPFS 公有网络文件互传演示

## 一、载入压缩包并运行镜像

进入压缩包文件目录，载入压缩包，并分别运行 ipfs_node0和ipfs_node1镜像

```
docker load --input ipfs_nodes.tar
```

```
docker run ipfs_node0:v1
docker run ipfs_node1:v1
```

log：

![image-20211216113455043](C:\Users\ThinkPad\AppData\Roaming\Typora\typora-user-images\image-20211216113455043.png)

查看已生成的镜像：

![image-20211216113535318](C:\Users\ThinkPad\AppData\Roaming\Typora\typora-user-images\image-20211216113535318.png)

可以看到已经生成3个镜像，其中ipfs_node0和ipfs_node1是我们部署的两个IPFS节点镜像，接下来我们要测试这两个镜像。

## 二、测试：

运行镜像 ipfs_node0:v1

```
docker run ipfs_node0:v1

```

镜像启动成功：

![image-20211216114342060](C:\Users\ThinkPad\AppData\Roaming\Typora\typora-user-images\image-20211216114342060.png)

运行镜像 ipfs_node1:v1

```
docker run ipfs_node1:v1
```

![image-20211216114404047](C:\Users\ThinkPad\AppData\Roaming\Typora\typora-user-images\image-20211216114404047.png)

查看运行的容器

![image-20211216114636587](C:\Users\ThinkPad\AppData\Roaming\Typora\typora-user-images\image-20211216114636587.png)

进入 ipfs_node0:v1 生成的容器查看ipfs version

```
docker exec -it 931921105bae /bin/sh  #进入ipfs_node0生成的容器
cat /data/ipfs/version # 查看ipfs 版本
```

内容为“11”

![image-20211216114937771](C:\Users\ThinkPad\AppData\Roaming\Typora\typora-user-images\image-20211216114937771.png)

通过node0发布文件，node1通过哈希值获取文件

```
ipfs add /data/ipfs/version
```

log:

```
added QmNtaCdRAmsR2cG4dvhfAc8eZv1kaGYoAPGZjec2KY4yG6 version
```

![image-20211216115022141](C:\Users\ThinkPad\AppData\Roaming\Typora\typora-user-images\image-20211216115022141.png)


用exit命令退出当前容器后，在进入另一台容器，上通过hash获取文件内容

```
docker exec -it a0a539929f24 /bin/sh
ipfs cat QmNtaCdRAmsR2cG4dvhfAc8eZv1kaGYoAPGZjec2KY4yG6
```

log:

```
11
```

![image-20211216115448623](C:\Users\ThinkPad\AppData\Roaming\Typora\typora-user-images\image-20211216115448623.png)

测试成功。

