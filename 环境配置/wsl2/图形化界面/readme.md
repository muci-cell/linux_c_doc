## 首先配置WSL2：

**1** 以管理身份打开Windows powershell（如果没有可以从Microsoft Store下载Windows terminal安装）并输入命令启用WSL功能：

```text
命令: dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

**2** 在Windows Powershell输入命令启用“虚拟机平台”功能

```text
命令：dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

**3** 下载适用于 x64 计算机的 WSL2 Linux 内核更新包并安装：

[https://docs.microsoft.com/zh-cn/windows/wsl/install-manual#step-4—download-the-linux-kernel-update-package](https://link.zhihu.com/?target=https%3A//docs.microsoft.com/zh-cn/windows/wsl/install-manual%23step-4---download-the-linux-kernel-update-package)

**4** 在Windows Powershell输入命令设置WSL版本为 WSL2

```text
命令: wsl --set-default-version 2
```

**5** 在Microsoft Store选择喜欢的Ubuntu发行版本安装。也可以在Windows Powershell输入命令下载安装：

```text
命令: wsl --install
```

**6** 安装完成后输入用户名/密码完成注册。记得设置root密码：

```text
命令: sudo passwd root
```

**7** 卸载wsl：①在360软件卸载Ubuntu。②在Windows powershell中输入wsl -l -v查看 版本号 和wsl --unregister Ubuntu-xxx注销对应版本。

## 配置图形化界面：

**1** 下载和安装VcXsrv安装：

[https://**sourceforge.net/project**s/vcxsrv/](https://link.zhihu.com/?target=https%3A//sourceforge.net/projects/vcxsrv/)

**2** 配置过程：**①**启动XLaunch **②** One large window **③** start no client **④** 所有选项选中 **⑤** Save configuration到Windows桌面作为每次 启动VcXsrv的永久设置文件**config.xlaunch**

**3** 在Ubuntu terminal输入命令安装xfce4功能 (如果提示错误可以通过 sudo apt-get update):

```text
命令: sudo apt install -y xfce4
```

**4** 在Ubuntu terminal 输入命令配置通信协议：

①在Windows Powershell输入命令查询以太网适配器 vEthernet (WSL)的IPv4地址：

```text
命令: ipconfig
```

②输入命令编辑resolv.conf文件中的网卡设置：

```text
命令 : sudo vim /etc/resolv.conf
修改resolv.conf文件内容为(记得前面都没有注释#)：
 [network]
 generateResolvConf = false
 nameserver 172.21.160.1
```

③输入命令编辑bashrc文件：

```text
命令：vim ~/.bashrc
最后一行添加:
export DISPLAY=172.21.160.1:0
export WAYLAND_DISPLAY=$DISPLAY
然后输入命令：
source ~/.bashrc
```

**5** 每次启动图形化桌面流程为：①打开config.xlaunch ②打开Ubuntu terminal中输入命令启动图形化界面：

```text
 startxfce4
```

*Tips:* *由于`WSL2`其实是用`Hyper-V`技术实现的一个虚拟机,和`WSL1`的工作原理不一样,因此如果使用之前网上的方法直接设置`DISPLAY=:0.0`的话,启动xfce4的时候会出现错误。常见故障诊断见：*

*防火墙问题和bashrc设置问题:* [Dtouch：WSL2下startxfce4报错](https://zhuanlan.zhihu.com/p/587868390)

## 配置VScode程序开发环境:

**1** 从下面连接依次安装vscode及扩展程序：

①[Download Visual Studio Code - Mac, Linux, Windows](https://link.zhihu.com/?target=https%3A//code.visualstudio.com/download)

②[Remote Development - Visual Studio Marketplace](https://link.zhihu.com/?target=https%3A//marketplace.visualstudio.com/items%3FitemName%3Dms-vscode-remote.vscode-remote-extensionpack)

完成后输入命令更新vscode启动所需要的库:

```text
sudo apt-get update
```

**2** 从Ubuntu terminal输入一下命令启动vscode:

```text
code .
```

可以界面右下栏目选择的select interpreter功能，选择 WSL-python/ananconda(windows)-python 的base和虚拟环境编译代码。

Tips:在配置的环境中安装**yapf（**代码格式化工具**），[具体使用参考](https://link.zhihu.com/?target=https%3A//blog.csdn.net/eastyell/article/details/104696619%3Fops_request_misc%3D%25257B%252522request%25255Fid%252522%25253A%252522166117937016782391814651%252522%25252C%252522scm%252522%25253A%25252220140713.130102334..%252522%25257D%26request_id%3D166117937016782391814651%26biz_id%3D0%26utm_medium%3Ddistribute.pc_search_result.none-task-blog-2~all~top_positive~default-2-104696619-null-null.142%255Ev42%255Epc_rank_34_ecpm25%2C185%255Ev2%255Econtrol%26utm_term%3Dvscode%25E9%2585%258D%25E7%25BD%25AEpython%26spm%3D1018.2226.3001.4187)。**[然后在File->Preferences->Settings，输入python.formatting.provider；](https://link.zhihu.com/?target=https%3A//blog.csdn.net/Pythonlaowan/article/details/99205649)使用快捷键：**Alt+Shift+F**调用代码整理工作。

[安装flake8](https://link.zhihu.com/?target=https%3A//cloud.tencent.com/developer/article/2131871)**（**会检查编写代码时的不规范的地方和语法错误**）**cmd调用命令： flake8 文件名

**记得配置vscode工作区域为（ctrl+shift+P输入**setting.json**）：**

```text
{
    "python.linting.flake8Enabled": true,
    "python.formatting.provider": "yapf",
    "python.linting.flake8Args": ["--max-line-length=248"],
    "python.linting.pylintEnabled": false
}
```
