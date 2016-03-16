## Technical FAQ and Troubleshooting

1. No such file or director, when running on SELinux 
 If you have `SELinux` enabled, you may get the following error message : 
 ```
 # docker run --name mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw  --volume-driver=pxd -v sql_vol:/var/lib/mysql -d mysql
 docker: Error response from daemon: no such file or directory.
 See 'docker run --help'.
 ```
 This can be remedied as follows:
 ```
 # docker run  --security-opt=label:disable  --name mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw  --volume-driver=pxd -v  sql_vol:/var/lib/mysql -d mysql
 ```
 You will not need to workaround this after [20834](https://github.com/docker/docker/pull/20834) is merged

2. Pxctl show persmission denied
 If you run a pxctl command and get the error like the below, the issue is that you need to run as root to use the pxctl tools. This is a temporary issue, as pxctl will move to a non-priviledged mode.
 ```
 pxctl show cluster
 show cluster: Get http://unix.sock/v1/cluster/enumerate: dial unix /var/lib/osd/cluster/osd.sock: connect: permission denied
  ```
 To enable root, you can run  ```sudo su ```. 

