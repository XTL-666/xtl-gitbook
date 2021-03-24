# windows10深度学习环境配置

先放一张成果图

成果图



1.anaconda下载，从官网正常下，用迅雷速度挺快。附上下载地址 anaconda for windows

需注意：安装过程中，有个Add anaconda to my PATH environment variable,记得选上。

anaconda

最后，在开始菜单搜索anaconda，有的话就可了，安装成功。

2.安装CUDA和cudnn，这个需要科学上网，得有谷歌号（别着急关掉），很麻烦，我自己搞了个科学上网，这俩下了下来，但不能全部适用。

GPU

首先找到你的英伟达驱动，查看gpu型号所对应的CUDA，这个是向下兼容的，也就是说，他说适应的版本及其以下都行，我给的这个链接11.0以下都可以用。打开它

找到组件，这里显示的是 CUDA 11.1.114 说明这个版本以下都可以用。链接：CUDA 和cudnn 提取码：2qkx

cuda的安装，我自己安装的时候出了点问题，第一次安装电脑自动重启了，第二次装就好了。

CUDA

cmd 命令行 敲 nvcc -V

如果出现上图这样就成功了。

接下来是cudnn，下载完成后，将压缩包解压后，把里面的三个文档夹里面的文档放到CUDA9安装目录相应文档夹下即可\(一般安装的目录是C:\Program Files\NVIDIA GPU Computing Toolkit\)。这三个是完全覆盖掉里面的，也就是替换。我在这个装C盘的，

这是博主的路径，第一次装的时候留下了遗留文档，一直没找到那个路径，在C盘里搜的关键字 NVIDA GPU 找到了。替换完成之后，在cmd里面 cd C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.1\extras\demo\_suite（就是刚才替换文档夹的路径了），然后分别敲两个 deviceQuery.exe 和 bandwithTest.exe。如果以上两步都返回了Result=PASS，那么就算成功了！

到此，cuda和cudnn的安装结束。

3.安装pytorch，tensorflow等等，这个需要给windows换个源，具体是

\(1\)在windows文档管理器中,输入 %APPDATA%

\(2\)会定位到一个新的目录下，在该目录下新建pip文档夹，然后到pip文档夹里面去新建个pip.ini文档

\(3\)在新建的pip.ini文档中输入以下内容

\[global\]

timeout = 6000

index-url = https://pypi.tuna.tsinghua.edu.cn/simple

trusted-host = pypi.tuna.tsinghua.edu.cn

或者是 阿里的源 我用的是阿里的

\[global\]

index-url=http://mirrors.aliyun.com/pypi/simple/

\[install\]

trusted-host=mirrors.aliyun.com

换好之后 reboot

reboot之后，cmd 敲 pip install tensorflow

或者打开 pytroch 官网 https://pytorch.org/

cmd敲 PIP下的你装的CUDA版本

安装完成之后，敲 import torch

 print（torch.\_\_version\_\_\)

 print\(‘ gpu ：’，torch.cuda.is\_available\(\)\)

得到正确的输出就行了 ，True。

这里需要注意一点，有的需要安装VC的缺失内容，你根据报错提示的链接内容下载就行，速度很快

至此，安装结束。

4.为vscode设置工作区

打开之后shift+ctrl+p找到你的anaconda的路径，

正常设置，博主这里是python3.8.5,至此全部完成。

注意：我这里把我自己电脑里装的python卸载装的anaconda里面的python，所以用的话设置的话也是anaconda里面的python.exe。有人用pycharm，我的pycharm弄了很多回，总是弄不好，就想到了用vscode来设置。

