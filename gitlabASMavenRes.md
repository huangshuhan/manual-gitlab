将gitlab作为Maven库的原理  
下面介绍一些maven仓库工作的原理。典型的一个maven依赖下会有这三个文件：  
maven-metadata.xml  
maven-metadata.xml.md5  
maven-metadata.xml.sha1  
maven-metadata.xml里面记录了最后deploy的版本和时间。  
其中md5, sha1校验文件是用来保证这个meta文件的完整性。  
maven在编绎项目时，会先尝试请求maven-metadata.xml，如果没有找到，则会直接尝试请求到jar文件，在下载jar文件时也会尝试下载jar的md5, sha1文件。  
maven-metadata.xml文件很重要，如果没有这个文件来指明最新的jar版本，那么即使远程仓库里的jar更新了版本，本地maven编绎时用上-U参数，也不会拉取到最新的jar。  
根据这个原理，我们只要把jar以及相应的jar的md5和sha1文件(如果没有的md5和sha1话，只需要放jar包也可以)，放入命名规则的文件夹里，上传到gitlab上。  
需要用到依赖的项目在配置pom.xml，增加这段配置。  
《repositories》  
		《repository》  
			《id》maggandalf-maven-repository《/id》  
			《url》http://192.168.11.20/gitlab/test/test_mvn/raw/master/res《/url》  
		《/repository》  
《/repositories》  

其中test是账号名，test_mvn是repository名。  
注意: http://192.168.11.20/gitlab/test/test_mvn/blob/master/res/dom4j/dom4j/1.6/dom4j-1.6.jar  由于gitlab对下载地址作了保护，这个地址并非下载地址，而是是jar包的url地址。而在配置pom.xml时，要使用下载地址。  
http://192.168.11.20/gitlab/test/test_mvn/raw/master/res/dom4j/dom4j/1.6/dom4j-1.6.jar  这个才是下载地址。  
 
