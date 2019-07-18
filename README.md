# Jenkins REST API 总结
<div>
<b>阅读须知：</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如果未做特别说明<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;文中所有的“jobName”指的是任务的名称<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;文中所有的“viewName”指的是任务所在的视图名称<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;文中所有的“fileName”指的是任务所在的文件夹名称<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;文中所有的“oldJobName”指的是重命名操作之前的任务名<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;文中所有的“newJobName”指的是重命名操作成功之后的任务名<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;其他参数命名遵从以上规则<br/>
<b>特别说明：</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;虽然POST类型的请求可以将参数直接放在URL中，但是不建议这样使用<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这样做可能会影响到安全，也破坏了POST的设计，如果使用请保证数据安全
</div>

一、任务类(job)

1、创建job	http请求类型：post
*  (1)、在Jenkins主页创建任务<br/>
  http://localhost:8080/jenkins/createItem?name=jobName
*  (2)、在指定文件夹中创建任务<br/>
  http://localhost:8080/jenkins/job/fileName/createItem?name=jobName
*  (3)、在指定视图中创建任务<br/>
  http://localhost:8080/jenkins/view/viewName/createItem?name=jobName

2、获取config	http请求类型：get
*  (1)、任务未在任何文件夹中<br/>
  http://localhost:8080/jenkins/job/jobName/config.xml
*  (2)、任务被创建在文件夹中<br/>
  http://localhost:8080/jenkins/job/fileName/job/jobName/config.xml

3、构建job	http请求类型：post
*  (1)、任务未在任何文件夹中<br/>
  http://localhost:8080/jenkins/job/jobName/build
*  (2)、任务被创建在文件夹中<br/>
  http://localhost:8080/jenkins/job/fileName/job/jobName/build

4、删除job	http请求类型：post
*  (1)、任务未在任何文件夹中<br/>
  http://localhost:8080/jenkins/job/jobName/doDelete
*  (2)、任务被创建在文件夹中<br/>
  http://localhost:8080/jenkins/job/fileName/job/jobName/doDelete

5、任务重命名	http请求类型：post
*  (1)、任务未在任何文件夹中<br/>
  http://localhost:8080/jenkins/job/oldJobName/doRename?newName=newJobName
*  (2)、任务被创建在文件夹中<br/>
  http://localhost:8080/jenkins/job/fileName/job/oldJobName/doRename?newName=newJobName

二、文件夹类(file)	(此处的fileName指代即将对其操作的文件夹的名称)

1、创建文件夹	http请求类型：post<br/>
  http://localhost:8080/jenkins/createItem?name=fileName
  
2、删除文件夹	http请求类型：post<br/>
  http://localhost:8080/jenkins/job/fileName/doDelete
  
3、文件夹重命名	http请求类型：post<br/>
  http://localhost:8080/jenkins/job/oldFileName/confirmRename?newName=newFileName
  
4、获取config	http请求类型：get<br/>
  http://localhost:8080/jenkins/job/jobName/config.xml

特别说明：
*  创建文件夹和删除文件夹的api和创建删除任务的api相同，
*  但是创建文件夹和创建任务时所涉及的xml文件内容有区别，
*  获取文件夹的config和获取任务的config可以写入同一个方法。

三、视图类(view)	(此处的viewName指代即将对其进行操作的视图的名称)

1、创建视图	http请求类型：post<br/>
  http://localhost:8080/jenkins/createView?name=viewName
  
2、删除视图	http请求类型：post<br/>
  http://localhost:8080/jenkins/view/viewName/doDelete
  
3、获取config	http请求类型：get<br/>
  http://localhost:8080/jenkins/view/viewName/config.xml

当然，此处的API整理还不够完整，后续会持续进行更新
