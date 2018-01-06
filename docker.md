# Docker常用命令   
- docker ps XXX 显示当前正在运行的容器
- docker ps -a XXX 显示所有的容器
- docker inspect XXX 显示容器详情，基本所有信息都有
- docker logs XXX 显示容器的启动日志（这个特别强调，除了我们说的把容器日志挂载出来还可以查看这个日志。区别：挂载出来的是程序自己的日志，这个是容器的启动日志，小编有好几次线上出bug都是通过这个命令找到原因！）
- docker images 显示日志列表
- docker stop XXX 停止容器
- docker start XX 开启容器
- docker restart XXX 重启容器
- docker rm XXX 删除已经停止的容器（正在运行的删不了）
- docker rm -f XXX 删除容器（停止、运行的容器）
- docker exec -it XXX /bin/bash 进入容器内部
- docker cp XXX：要拷贝的文件在容器里面的路径 要拷贝到宿主机的相应路径（从容器里拷贝文件到主机）
- docker cp 要拷贝到宿主机的相应路径 XXX：要拷贝的文件在容器里面的路径（从主机拷贝文件到容器里）
- docker export XXX > test.tar 导出容器
- sudo docker import - test/tomcat:1.0.1 导入容器
- docker search tomcat 查找tomcat的docker官方镜像
- docker search RepositoryIP:5000/ 查找某个仓库上的镜像
- docker pull 镜像名 （拉取镜像）
- docker tag 镜像ID 名字:版本 （修改镜像名字）
- docker events --since="1467302400" （查看docker时间，since按时间戳，f按条件，）
- docker push 镜像名:版本 推送你的镜像到你的仓库或者github上
---

# 安装本地仓库     
1. 拉取仓库镜像
`docker pull registry`
2. 启动仓库
`docker run -d -p 5000:5000 -v /opt/data/registry:/tmp/registry registry`
3. 修改镜像的标签
`docker tag OldName LocalRepositoryIP:5000/NewName`
4. 将镜像上传到本地仓库
`docker push LocalRepositoryIP:5000/TagName`     
   
#### *如果本地push出错，centos 6.5 需要修改/etc/sysconfig/docker文件，在OPTIONS里面追加参数：`--insecure-registry 10.18.1.99:5000`默认是从远程拉取镜像的，如果需要默认从本地拉取，那么需要再追加启动参数：`--add-registry=10.18.1.99:5000`* </br>
---

# Docker命令详细说明      
- Docker Run命令，启动参数</br>
当我们启动一个容器时，首先需要确定这个容器是运行在前台还是运行在后台。</br>
*后台模式：* 如果在docker run后面追加-d=true或者-d，那么容器将会运行在后台模式，并打印新容器ID。此时所有I/O数据只能通过网络资源或者共享卷组来进行交互。因为容器不再监听你执行docker run的这个终端命令行窗口。但你可以通过执行docker attach来重新附着到该容器的回话中。需要注意的是，容器运行在后台模式下，是不能使用--rm选项的。</br>
*前台模式：* 不指定-d参数即可，Docker会在容器中启动进程，同时将当前的命令行窗口附着到容器的标准输入、标准输出和标准错误中。也就是说容器中所有的输出都可以在当前窗口中看到。甚至它都可以虚拟出一个TTY窗口，来执行信号中断。这一切都是可以配置的：</br>
`-a=[]          　	: Attach to 'STDIN', 'STDOUT' and/or 'STDERR'`</br>
如果在执行run命令时没有指定-a参数，那么Docker默认会挂载所有标准数据流，包括输入输出和错误，你可以单独指定挂载哪个标准流。</br>
`$ sudo docker run -a stdin -a stdout -i -t ubuntu /bin/bash`</br>
`-t=false			: Allocate a pseudo-tty` </br>
`--sig-proxy=true	: Proxify all received signal to the process (non-TTY mode only)`</br>
`-i=false			: Keep STDIN open even if not attached`</br>
如果要进行交互式操作（例如Shell脚本），那我们必须使用-i -t参数同容器进行数据交互。但是当通过管道同容器进行交互时，就不需要使用-t参数，例如下面的命令：</br>
`echo test | docker run -i busybox cat`</br>
---


