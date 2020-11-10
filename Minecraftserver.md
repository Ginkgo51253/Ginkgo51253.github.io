---
title: "How to build your own Minecraft server"
permalink: "/Minecraftserver/"
---

Return to [Home page](https://Ginkgo51253.github.io/Home)

---

# 如何建立自己的私人Minecraft服务器

## 你需要的东西

1. 一个云服务器（本地的也行，但需要域名来让服务器能在公网访问到）。最好使用Linux系统（windows也行）。为了更流畅的体验，建议使用i3以上的服务器处理器，4g以上的内存（如果游玩人数较多请优先考虑升级内存）。
2. Minecraft服务器版本。如果是原版Minecraft，可以前往Minecraft官网进行下载，如果要搭载mod，可以前往Forge官网进行下载。原版与Forge版本的安装方法一致，不需要额外的操作。
3. Minecraft客户端版本。客户端版本需要和你服务器版本的版本对应。
4. 一些一起玩的好友。这个如果没有你为什么要架设私人服务器？

## 架设方法

1. 登录云服务器，检查Java环境（推荐使用jdk1.8，低版本Java不兼容，高版本Minecraft不一定能兼容），如果在linux下，输入```java -v```查看java版本，如果没有安装，请先安装Java环境

2. 将你下载好的Minecraft服务端文件上传至云服务器，按以下指令格式填入本地文件路径、服务器用户名、服务器IP地址以及你要存放文件的路径，即可将本地文件上传至云端

   ```
   scp 本地文件路径 服务器用户名@服务器IP地址:服务器存放路径
   ```

3. 第一次打开服务端Minecraft，将目录切换到有Minecraft服务端文件的目录，输入```./你的Minecraft服务端文件名称```来第一次运行。第一次打开时是无法成功运行的，因为运行时目录下会新产生一个eula文件（许可证），进入这个文件将```eula=false```修改为```eula=true```。

4. 第二次打开服务端Minecraft，方法同上，如果你的Java环境配置没有问题，服务端将顺利启动并开始建立你的服务器世界，建立完毕后可以在控制台输入一些控制台指令来进行管理。

5. 打开你在本地的Minecraft客户端，在多人游戏界面选择添加服务器，输入你云服务器的IP地址，如果网络连接没有问题，一会便能连接上你的Minecraft服务器。

## 额外配置

1. 服务器后台运行。输入```nohup ./你的Minecraft &```使你的Minecraft脱离控制台运行，此时即便你关闭控制台，只要云服务器还在正常工作，你始终都能从本地客户端连接到你的云服务器。
2. 查看Minecraft命令，使用控制台打开Minecraft服务端，输入help查看Minecraft命令，记得给自己添加管理员权限
3. 配置Mod，从Forge官网或其他网站下载需要Forge运行的mod，注意关注mod发布者是否说明联机可用，将mod上传至服务器的mod文件夹，之后再在客户端的mod中也添加这个mod，只要服务器和本地都能成功运行，则你可用连接到服务器使用这个mod

---

Return to [Home page](https://Ginkgo51253.github.io/Home)