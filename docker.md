

=====================================================��װ���زֿ�============================================================
##��ȡ�ֿ⾵��
docker pull registry
##�����ֿ�
docker run -d -p 5000:5000 -v /opt/data/registry:/tmp/registry registry
##�޸ľ���ı�ǩ
docker tag OldName LocalRepositoryIP:5000/NewName
##�������ϴ������زֿ�
docker push LocalRepositoryIP:5000/TagName
##����ĳ���ֿ�ľ���
docker search RepositoryIP:5000/


##˵��
�������push����centos 6.5 ��Ҫ�޸�/etc/sysconfig/docker�ļ�����OPTIONS����׷�Ӳ�����--insecure-registry 10.18.1.99:5000
Ĭ���Ǵ�Զ����ȡ����ģ������ҪĬ�ϴӱ�����ȡ����ô��Ҫ��׷������������--add-registry=10.18.1.99:5000 

=============================================================================================================================

======================================================Docker Run����=========================================================
##########��������˵��##########
����������һ������ʱ��������Ҫȷ�����������������ǰ̨���������ں�̨��
-d=false: Detached mode: Run container in the background, print new container id
Detached (-d)
�����docker run����׷��-d=true����-d����ô�������������ں�̨ģʽ����ʱ����I/O����ֻ��ͨ��������Դ���߹�����������н�������Ϊ�������ټ�����ִ��docker run������ն������д��ڡ��������ͨ��ִ��docker attach�����¸��ŵ��������Ļػ��С���Ҫע����ǣ����������ں�̨ģʽ�£��ǲ���ʹ��--rmѡ��ġ�
Foregroud
��ǰ̨ģʽ�£���ָ��-d�������ɣ���Docker�����������������̣�ͬʱ����ǰ�������д��ڸ��ŵ������ı�׼���롢��׼����ͱ�׼�����С�Ҳ����˵���������е�����������ڵ�ǰ�����п����������������������һ��TTY���ڣ���ִ���ź��жϡ���һ�ж��ǿ������õģ�
-a=[]          ��	: Attach to `STDIN`, `STDOUT` and/or `STDERR`
-t=false			: Allocate a pseudo-tty
--sig-proxy=true	: Proxify all received signal to the process (non-TTY mode only)
-i=false			: Keep STDIN open even if not attached
�����ִ��run����ʱû��ָ��-a��������ôDockerĬ�ϻ�������б�׼��������������������ʹ�������Ե���ָ�������ĸ���׼����
$ sudo docker run -a stdin -a stdout -i -t ubuntu /bin/bash
���Ҫ���н���ʽ����������Shell�ű����������Ǳ���ʹ��-i -t����ͬ�����������ݽ��������ǵ�ͨ���ܵ�ͬ�������н���ʱ���Ͳ���Ҫʹ��-t������������������
echo test | docker run -i busybox cat

=============================================================================================================================


=======================================================Docker��������========================================================
docker ps XXX ��ʾ��ǰ�������е�����
docker ps -a XXX ��ʾ���е�����
docker inspect XXX ��ʾ�������飬����������Ϣ����
docker logs XXX ��ʾ������������־������ر�ǿ������������˵�İ�������־���س��������Բ鿴�����־�����𣺹��س������ǳ����Լ�����־�������������������־��С���кü������ϳ�bug����ͨ����������ҵ�ԭ�򣡣�
docker images ��ʾ��־�б�
docker stop XXX ֹͣ����
docker start XX ��������
docker restart XXX ��������
docker rm XXX ɾ���Ѿ�ֹͣ���������������е�ɾ���ˣ�
docker rm -f XXX ɾ��������ֹͣ�����е�������
docker exec -it XXX /bin/bash ���������ڲ�
docker cp XXX��Ҫ�������ļ������������·�� Ҫ����������������Ӧ·���������������ļ���������
docker cp Ҫ����������������Ӧ·�� XXX��Ҫ�������ļ������������·���������������ļ��������
docker export XXX > test.tar ��������
sudo docker import - test/tomcat:1.0.1 ��������
docker search tomcat ����tomcat��docker�ٷ�����
docker pull ������ ����ȡ����
docker tag ����ID ����:�汾 ���޸ľ������֣�
docker events --since="1467302400" ���鿴dockerʱ�䣬since��ʱ�����f����������
docker push ������:�汾 ������ľ�����Ĳֿ����github��
=============================================================================================================================
=====Run GitLab Runner in a container
docker run -d --name gitlab-runner --restart always -v /srv/gitlab-runner/config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock gitlab/gitlab-runner:latest

