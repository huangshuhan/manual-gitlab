Gitlab官网一键安装配置以及修改相对路径  
前言：由于安装gitlab并不是单纯的一个服务，他需要mysql,redis,ruby等很多其他服务，才能一起完成运行。而要将这些服务全部安装，然后一一配置，还涉及到权限、版本问题，所以官网提供了一个一键配置的安装包。它将所有服务都一次安装、配置好，如果不太懂运维的同学，使用这个方法也是非常容易的。不太好的地方可能就是不太灵活。  
一、	安装gitlab  
官网安装教程链接地址: https://about.gitlab.com/downloads/  
选择合适的linux操作系统，按照官方的安装教程，就可以安装成功，没什么大的问题。  
二、	修改gitlab相对路径  
Gitlab安装成功以后，只要输入ip即可访问，但我们想改成ip/gitlab的访问路径怎么办呢。  
官方的链接地址: http://docs.gitlab.com/omnibus/settings/configuration.html  
里面的Enable relative URL in Gitlab此项说明了，如何更改相对路径，就是修改/etc/gitlab/ gitlab.rb下的external_url这个值,更改需要注意的问题是以下几点:  
1. external_url 修改时，注意不要使用官网的https，因为都没开通这个协议，除非开通了相关的https协议。  
2.不要使用root用户去进行相关的操作.  
由于我们是局域网，我配置的external_url 'http://localhost/gitlab'，配置完成以后就可以利用ip/gitlab的访问路径进行访问了。
