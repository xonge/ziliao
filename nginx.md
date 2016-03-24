1. centos平台编译环境使用如下指令
   
   安装make：
   
   yum -y install gcc automake autoconf libtool make
   安装g++:
   
   yum install gcc gcc-c++
   
2. 一般我们都需要先装pcre, zlib，前者为了重写rewrite，后者为了gzip压缩。
   1.选定源码目录
   可以是任何目录，本文选定的是/usr/local/src
   
   cd /usr/local/src
   2.安装PCRE库
   ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/ 下载最新的 PCRE 源码包，使用下面命令下载编译和安装 PCRE 包：
   
   cd /usr/local/src
   wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.34.tar.gz 
   tar -zxvf pcre-8.34.tar.gz
   cd pcre-8.34
   ./configure
   make
   make install
   
3. 3.安装zlib库
   http://zlib.net/zlib-1.2.8.tar.gz 下载最新的 zlib 源码包，使用下面命令下载编译和安装 zlib包：
   
   cd /usr/local/src
   
   wget http://zlib.net/zlib-1.2.8.tar.gz
   tar -zxvf zlib-1.2.8.tar.gz
   cd zlib-1.2.8
   ./configure
   make
   make install
   
4. 4.安装ssl（某些vps默认没装ssl)
   
   cd /usr/local/src
   wget http://www.openssl.org/source/openssl-1.0.1c.tar.gz
   tar -zxvf openssl-1.0.1c.tar.gz
   
5. 5.安装nginx
   
   Nginx 一般有两个版本，分别是稳定版和开发版，您可以根据您的目的来选择这两个版本的其中一个，下面是把 Nginx 安装到 /usr/local/nginx 目录下的详细步骤：
   
   cd /usr/local/src
   wget http://nginx.org/download/nginx-1.4.2.tar.gz
   tar -zxvf nginx-1.4.2.tar.gz
   cd nginx-1.4.2
   
   ./configure --sbin-path=/usr/local/nginx/nginx 
   --conf-path=/usr/local/nginx/nginx.conf 
   --pid-path=/usr/local/nginx/nginx.pid 
   --with-http_ssl_module 
   --with-pcre=/usr/local/src/pcre-8.34 
   --with-zlib=/usr/local/src/zlib-1.2.8 
   --with-openssl=/usr/local/src/openssl-1.0.1c
   
   make
   make install
   --with-pcre=/usr/src/pcre-8.34 指的是pcre-8.34 的源码路径。
   --with-zlib=/usr/src/zlib-1.2.7 指的是zlib-1.2.7 的源码路径。
   
   安装成功后 /usr/local/nginx 目录下如下
   
   fastcgi.conf            koi-win             nginx.conf.default
   fastcgi.conf.default    logs                scgi_params
   fastcgi_params          mime.types          scgi_params.default
   fastcgi_params.default  mime.types.default  uwsgi_params
   html                    nginx               uwsgi_params.default
   koi-utf                 nginx.conf          win-utf
   
6. 6.启动
   确保系统的 80 端口没被其他程序占用，运行/usr/local/nginx/nginx 命令来启动 Nginx，
   
   netstat -ano|grep 80
   如果查不到结果后执行，有结果则忽略此步骤（ubuntu下必须用sudo启动，不然只能在前台运行）
   
   sudo /usr/local/nginx/nginx
   打开浏览器访问此机器的 IP，如果浏览器出现 Welcome to nginx! 则表示 Nginx 已经安装并运行成功。
   
   
   
   -----------------------------------------------------
   到这里nginx就安装完成了，如果只是处理静态html就不用继续安装了
   
   如果你需要处理php脚本的话，还需要安装php-fpm。
   
   下面安装排错
   
   附：可能遇到的错误和一些帮助信息
   
   1.1编译pcre错误
   
   libtool: compile: unrecognized option `-DHAVE_CONFIG_H'
   libtool: compile: Try `libtool --help' for more information.
   make[1]: *** [pcrecpp.lo] Error 1
   make[1]: Leaving directory `/usr/local/src/pcre-8.34'
   make: *** [all] Error 2
   
   
   解决办法：安装g++,别忘了重新configure
   
   apt-get install g++
   apt-get install build-essential
   make clean
   ./configure
   make
   
   1.2 make出错
   
   make: *** No rule to make target `build', needed by `default'.  Stop.
   ./configure: error: SSL modules require the OpenSSL library.
   You can either do not enable the modules, or install the OpenSSL library
   into the system, or build the OpenSSL library statically from the source
   with nginx by using --with-openssl= option.
   按照第4步的安装方法或
   ubuntu下
   
   apt-get install openssl
   apt-get install libssl-dev
   centos下
   
   yum -y install openssl openssl-devel
   
   2.nginx编译选项
   
   make是用来编译的，它从Makefile中读取指令，然后编译。
   
   make install是用来安装的，它也从Makefile中读取指令，安装到指定的位置。
   
   configure命令是用来检测你的安装平台的目标特征的。它定义了系统的各个方面，包括nginx的被允许使用的连接处理的方法，比如它会检测你是不是有CC或GCC，并不是需要CC或GCC，它是个shell脚本，执行结束时，它会创建一个Makefile文件。nginx的configure命令支持以下参数：
   
   --prefix=path    定义一个目录，存放服务器上的文件 ，也就是nginx的安装目录。默认使用 /usr/local/nginx。
   --sbin-path=path 设置nginx的可执行文件的路径，默认为  prefix/sbin/nginx.
   --conf-path=path  设置在nginx.conf配置文件的路径。nginx允许使用不同的配置文件启动，通过命令行中的-c选项。默认为prefix/conf/nginx.conf.
   --pid-path=path  设置nginx.pid文件，将存储的主进程的进程号。安装完成后，可以随时改变的文件名 ， 在nginx.conf配置文件中使用 PID指令。默认情况下，文件名 为prefix/logs/nginx.pid.
   --error-log-path=path 设置主错误，警告，和诊断文件的名称。安装完成后，可以随时改变的文件名 ，在nginx.conf配置文件中 使用 的error_log指令。默认情况下，文件名 为prefix/logs/error.log.
   --http-log-path=path  设置主请求的HTTP服务器的日志文件的名称。安装完成后，可以随时改变的文件名 ，在nginx.conf配置文件中 使用 的access_log指令。默认情况下，文件名 为prefix/logs/access.log.
   --user=name  设置nginx工作进程的用户。安装完成后，可以随时更改的名称在nginx.conf配置文件中 使用的 user指令。默认的用户名是nobody。
   --group=name  设置nginx工作进程的用户组。安装完成后，可以随时更改的名称在nginx.conf配置文件中 使用的 user指令。默认的为非特权用户。
   --with-select_module --without-select_module 启用或禁用构建一个模块来允许服务器使用select()方法。该模块将自动建立，如果平台不支持的kqueue，epoll，rtsig或/dev/poll。
   --with-poll_module --without-poll_module 启用或禁用构建一个模块来允许服务器使用poll()方法。该模块将自动建立，如果平台不支持的kqueue，epoll，rtsig或/dev/poll。
   --without-http_gzip_module — 不编译压缩的HTTP服务器的响应模块。编译并运行此模块需要zlib库。
   --without-http_rewrite_module  不编译重写模块。编译并运行此模块需要PCRE库支持。
   --without-http_proxy_module — 不编译http_proxy模块。
   --with-http_ssl_module — 使用https协议模块。默认情况下，该模块没有被构建。建立并运行此模块的OpenSSL库是必需的。
   --with-pcre=path — 设置PCRE库的源码路径。PCRE库的源码（版本4.4 - 8.30）需要从PCRE网站下载并解压。其余的工作是Nginx的./ configure和make来完成。正则表达式使用在location指令和 ngx_http_rewrite_module 模块中。
   --with-pcre-jit —编译PCRE包含“just-in-time compilation”（1.1.12中， pcre_jit指令）。
   --with-zlib=path —设置的zlib库的源码路径。要下载从 zlib（版本1.1.3 - 1.2.5）的并解压。其余的工作是Nginx的./ configure和make完成。ngx_http_gzip_module模块需要使用zlib 。
   --with-cc-opt=parameters — 设置额外的参数将被添加到CFLAGS变量。例如,当你在FreeBSD上使用PCRE库时需要使用:--with-cc-opt="-I /usr/local/include。.如需要需要增加 select()支持的文件数量:--with-cc-opt="-D FD_SETSIZE=2048".
   --with-ld-opt=parameters —设置附加的参数，将用于在链接期间。例如，当在FreeBSD下使用该系统的PCRE库,应指定:--with-ld-opt="-L /usr/local/lib".
   典型实例(下面为了展示需要写在多行，执行时内容需要在同一行)
   
   ./configure
       --sbin-path=/usr/local/nginx/nginx
       --conf-path=/usr/local/nginx/nginx.conf
       --pid-path=/usr/local/nginx/nginx.pid
       --with-http_ssl_module
       --with-pcre=../pcre-4.4
       --with-zlib=../zlib-1.1.3
       
yum install pcre-devel
进入安装目录，找到可行性文件nginx ，执行./nginx -t