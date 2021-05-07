# 下载Go

### 下载地址：
- Go官网下载地址：https://golang.org/dl/

- Go官方镜像站（推荐）：https://golang.google.cn/dl/

Windows平台和Mac平台推荐下载可执行文件版，Linux平台下载压缩文件版。

![](https://www.liwenzhou.com/images/Go/install_go_dev/download1.png)

# 安装Go
### Linux
linux安装比较简单，wget需要版本的go然后设置下环境变量就可以了，如果不是要在Linux平台敲go代码就不需要在Linux平台安装Go，我们开发机上写好的go代码只需要跨平台编译好之后就可以拷贝到Linux服务器上运行了，这也是go程序跨平台易部署的优势。

1，比如下载好go1.14.1.linux-amd64.tar.gz文件：

	wget https://dl.google.com/go/go1.14.1.linux-amd64.tar.gz

2，将下载好的文件解压到/usr/local目录下：

	tar -zxvf go1.14.1.linux-amd64.tar.gz -C /usr/local  

如果提示没有权限，加上sudo以root用户的身份再运行。执行完就可以在/usr/local/下看到go目录了。

3，配置环境变量：（环境变量具体的含义后面会介绍）   
Linux下有两个文件可以配置环境变量，其中/etc/profile是对所有用户生效的；$HOME/.profile是对当前用户生效的，根据自己的情况自行选择一个文件打开，添加如下两行代码，保存退出。

	export GOROOT=/usr/local/go
	export PATH=$PATH:$GOROOT/bin

修改/etc/profile后要重启生效，修改$HOME/.profile后使用source命令加载$HOME/.profile文件即可生效。 检查：

	~ go version
	go version go1.14.1 linux/amd64

### Mac
下载可执行文件版，直接点击下一步安装即可，默认会将go安装到/usr/local/go目录下。

![](https://www.liwenzhou.com/images/Go/install_go_dev/mac_install_go.png)

同样，安装完之后用go version检查一下即可。


### windows

比如，下载64位Win10系统 Go1.14.1安装包到本地。
![](https://www.liwenzhou.com/images/Go/install_go_dev/download2.png)

然后一路点击next,在需要设置go安装目录的时候，自己选择一个想要安装的目录即可，这个路径就是GOROOT。
比如：
![](https://www.liwenzhou.com/images/Go/install_go_dev/install02.png)

# Go环境变量

安装完go之后还需要设置GOPATH。这里我来解释一下几个名词的含义：

- **GOROOT：**
GOROOT 的值是 Go 安装目录，还有其自带标准库的位置，用户一般不需要设置GOROOT，默认情况下Go语言安装工具会将其设置为安装的目录路径。（Mac一般安装于/usr/local/go）。

- **GOBIN：**
go install后生成的可执行文件都放在bin目录下。不允许设置多个路径。可以为空。为空时则遵循“约定优于配置”原则，可执行文件放在各自GOPATH目录的bin文件夹中

- **GOPATH:**
Go工作环境中常常用到的一个很重要的环境变量（这种设计类似java）。具体用途：go命令常常需要用到的，如go run，go install， go get等。允许设置多个路径，和各个系统环境多路径设置一样，windows用“;”，linux（mac）用“:”分隔。

GOPATH是代码库所在目录，即工作区。工作区下分三个基础目录：

1. src:存放源代码(比如：.go .c .h .s等)   按照golang默认约定，go run，go install等命令的当前工作路径（即在此路径下执行上述命令）。
2. pkg:存放编译时生成的中间文件, 主要是 *.a 文件。用于存放通过 go install 命令安装后的代码包的归档文件。前提是代码包中必需包含 Go 库源码文件。归档文件是指那些名称以 “.a” 结尾的文件。
3. bin:主要存放build可执行文件。在工程经过 go build、go install 或 go get 等指令后，会将产生的二进制可执行文件放在 $GOPATH/bin 目录下。



		goWorkSpace     // goWorkSpace为GOPATH目录
		  -- bin
		     -- myApp1  // 编译生成
		     -- myApp2  // 编译生成
		     -- myApp3  // 编译生成
		  -- pkg
		  -- src
		     -- common 1
		     -- common 2
		     -- common utils ...
		     -- myApp1     // project1
		        -- models
		        -- controllers
		        -- others
		        -- main.go 
		     -- myApp2     // project2
		        -- models
		        -- controllers
		        -- others
		        -- main.go 
		     -- myApp3     // project3
		        -- models
		        -- controllers
		        -- others
		        -- main.go 



可用go env 可查看当前go环境变量。看下我windows电脑上的env。

    set GO111MODULE=on
	set GOARCH=amd64
	set GOBIN=
	set GOCACHE=C:\Users\shiqi\AppData\Local\go-build
	set GOENV=C:\Users\shiqi\AppData\Roaming\go\env
	set GOEXE=.exe
	set GOFLAGS=
	set GOHOSTARCH=amd64
	set GOHOSTOS=windows
	set GOINSECURE=
	set GOMODCACHE=C:\Users\shiqi\IdeaProjects\go\pkg\mod
	set GONOPROXY=
	set GONOSUMDB=
	set GOOS=windows
	set GOPATH=C:\Users\shiqi\IdeaProjects\go
	set GOPRIVATE=
	set GOPROXY=https://goproxy.cn
	set GOROOT=D:\Go
	set GOSUMDB=sum.golang.google.cn
	set GOTMPDIR=
	set GOTOOLDIR=D:\Go\pkg\tool\windows_amd64
	set GCCGO=gccgo
	set AR=ar
	set CC=gcc
	set CXX=g++
	set CGO_ENABLED=1
	set GOMOD=NUL
	set CGO_CFLAGS=-g -O2
	set CGO_CPPFLAGS=
	set CGO_CXXFLAGS=-g -O2
	set CGO_FFLAGS=-g -O2
	set CGO_LDFLAGS=-g -O2
	set PKG_CONFIG=pkg-config



## 编译器推荐

- GOLand（首推）
- VSCode


