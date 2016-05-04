安装
源码安装方法采用gitlab中文官网论坛一位管理者提供的。链接地址：

https://bbs.gitlab.cc/topic/35/gitlab-ce-8-7-%E6%BA%90%E7%A0%81%E5%AE%89%E8%A3%85%E6%89%8B%E5%86%8C-centos6-rehl6

根据地址里面提供的方法，一步一步将gitlab相关的服务配置完成主要包括git,ruby,go,mysql,redis,gitlab-ce.根据提供的方法将相关配置配置好。
Gitlab提供一个检查所有组件安装以及配置是否成功的命令(安装链接地址给出)，得出以下结果，说明安装所有组件成功。

Checking GitLab Shell ...

GitLab Shell version >= 2.7.2 ? ... OK (2.7.2)  
Repo base directory exists? ... yes  
Repo base directory is a symlink? ... no  
Repo base owned by git:git? ... yes  
Repo base access is drwxrws---? ... yes  
hooks directories in repos are links: ... can't check, you have no projects  
Running /home/git/gitlab-shell/bin/check  
Check GitLab API access: OK  
Check directories and files:  


        /home/git/repositories/: OK
        /var/opt/gitlab/.ssh/authorized_keys: OK


Test redis-cli executable: redis-cli 3.0.7  
Send ping to redis server: PONG  
gitlab-shell self-check successful

Checking GitLab Shell ... Finished

Checking Sidekiq ...

Running? ... yes
Number of Sidekiq processes ... 1

Checking Sidekiq ... Finished

Checking Reply by email ...

Reply by email is disabled in config/gitlab.yml

Checking Reply by email ... Finished

Checking LDAP ...

LDAP is disabled in config/gitlab.yml

Checking LDAP ... Finished

Checking GitLab ...

Git configured with autocrlf=input? ... yes  
Database config exists? ... yes  
All migrations up? ... yes    
Database contains orphaned GroupMembers? ... no  
GitLab config exists? ... yes  
GitLab config outdated? ... no  
Log directory writable? ... yes  
Tmp directory writable? ... yes  
Uploads directory setup correctly? ... skipped (no tmp uploads folder yet)  
Init script exists? ... yes  
Init script up-to-date? ... yes  
projects have namespace: ... can't check, you have no projects  
Redis version >= 2.8.0? ... yes  
Ruby version >= 2.1.0 ? ... yes (2.1.8)  
Your git bin path is "/usr/local/bin/git"  
Git version >= 2.7.3 ? ... yes (2.7.4)  
Active users: 4  

Checking GitLab ... Finished

sh-4.1$ sudo /etc/init.d/gitlab restart      
[sudo] password for git:   
Shutting down GitLab Unicorn  
Shutting down GitLab Sidekiq  
Shutting down gitlab-workhorse  


.
GitLab is not running.  
Starting GitLab Unicorn  
Starting GitLab Sidekiq  
Starting gitlab-workhorse  

The GitLab Unicorn web server with pid 13406 is running.  
The GitLab Sidekiq job dispatcher with pid 13457 is running.  
The gitlab-workhorse with pid 13442 is running. 
GitLab and all its components are up and running.  
sh-4.1$ sudo -u git -H bundle exec rake gitlab:check RAILS_ENV=production
Checking GitLab Shell ...

GitLab Shell version >= 2.7.2 ? ... OK (2.7.2)  
Repo base directory exists? ... yes  
Repo base directory is a symlink? ... no  
Repo base owned by git:git? ... yes  
Repo base access is drwxrws---? ... yes  
hooks directories in repos are links: ... can't check, you have no projects  
Running /home/git/gitlab-shell/bin/check  
Check GitLab API access: OK  
Check directories and files:   

        /home/git/repositories/: OK  
        /var/opt/gitlab/.ssh/authorized_keys: OK  

Test redis-cli executable: redis-cli 3.0.7  
Send ping to redis server: PONG  
gitlab-shell self-check successful  

Checking GitLab Shell ... Finished

Checking Sidekiq ...

Running? ... yes
Number of Sidekiq processes ... 1

Checking Sidekiq ... Finished

Checking Reply by email ...

Reply by email is disabled in config/gitlab.yml

Checking Reply by email ... Finished

Checking LDAP ...

LDAP is disabled in config/gitlab.yml

Checking LDAP ... Finished

Checking GitLab ...

Git configured with autocrlf=input? ... yes  
Database config exists? ... yes  
All migrations up? ... yes  
Database contains orphaned GroupMembers? ... no  
GitLab config exists? ... yes  
GitLab config outdated? ... no  
Log directory writable? ... yes  
Tmp directory writable? ... yes  
Uploads directory setup correctly? ... skipped (no tmp uploads folder yet)  
Init script exists? ... yes  
Init script up-to-date? ... yes  
projects have namespace: ... can't check, you have no projects  
Redis version >= 2.8.0? ... yes  
Ruby version >= 2.1.0 ? ... yes (2.1.8)  
Your git bin path is "/usr/local/bin/git"  
Git version >= 2.7.3 ? ... yes (2.7.4)  
Active users: 4  

Checking GitLab ... Finished


安装完成以后，在根据安装方法提供的nginx安装链接，将nginx安装以及配置好，输入服务器ip，即可访问gitlab首页

注:1.官网推荐使用数据库Postgresql，公司服务器采用的是mysql      
   2.注意关闭防火墙和selinux (关闭selinux在安装链接中已经给出)

总结

gitlab并不单纯只是一个服务，他是需要靠很多的服务来进行配合完成的。而所有的服务只要一个出问题，gitlab也运行不起来。源码安装gitlab时最好是刚安装过的linux系统，因为这样的linux系统会干净点。安装其他各个服务的版本要严格按照安装攻略的来，不要低于其说的版本。安装过程中要使用git用户来修改权限，不过若报权限问题的话，直接先去暂时修改为最大就好了，最后再来调整。只要根据安装攻略的步骤一步一步来，基本没什么问题。

我安装过程中主要出现的问题有：

1)	有些服务linux自带的，而且版本过低，所以都先卸载，但linux有时卸载不干净，导致有时候配置还是有问题，这个问题很严重，耽误的时间最多，所以一开始在干净的linux系统安装会好很多。   
2)	有时候git用户的权限过不去，就去将权限暂时改为最大，保证服务安装完成。   
3)	检查所有组件时，gitlab-shell的配置文件里的gitlab_url和gitlab的地址端口要保持一致，否则会报错。
