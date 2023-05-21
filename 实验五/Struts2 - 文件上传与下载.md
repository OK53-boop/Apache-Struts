1.
FileUpload
├── pom.xml
└── src
    └── main
        ├── java
        │   └── shiyanlou
        │       └── structs
        │           ├── DownloadAction.java
        │           ├── MultiUploadAction.java
        │           └── UploadAction.java
        ├── resources
        │   └── structs.xml
        └── webapp
            ├── error.jsp
            ├── index.jsp
            ├── success.jsp
            └── WEB-INF
                └── web.xml
                
                
这是一个基于Struts2框架的文件上传项目的目录结构。具体来说，该项目包含了以下文件和目录：

- pom.xml：Maven项目的配置文件，用于项目依赖和构建。
- src/main/java：Java源代码目录，包含了项目的所有Java类文件。
- shiyanlou/structsJava类文件的包名，其中包含了三个Struts2的Action类文件：DownloadAction.java、MultiUploadAction.java和UploadAction.java。
- resources/structs.xml：Struts2的配置文件，用于配置Action、拦截器、结果类型等。
- webapp：Web应程序的根目录，包含了所有的Web资源文件。
- error.jsp：上传文件出错时显示的错误页面。
- index.jsp：上传文件的表单页面。
- success.jsp：上传文件成功后显示的页面。
- WEB-INF/web.xml：Web应用程序的部署描述符用于配置Servlet、Filter、Listener等。









2.
wget http://labfile.oss.aliyuncs.com/courses/32/m2.zip
unzip m2.zip
mv .m2 /home/shiyanlou/

这是一组Linux命令，用于下载并安装Maven的配置文件。

具体来说，这组命令分为三个部分：

1. wget http://labfile.oss.aliyuncs.com/courses/32/m2.zip使用wget命令下载m2.zip文件，该文件包含了Maven的配置文件。

2. unzip m2.zip：使用unzip命令解压m2文件，将其中的配置文件提取出来。

3. mv .m2 /home/shiyanlou/：使用mv命令将提取出来的配置文件移动到/home/shiyanlou/目录下，这是Maven默认的配置文件存放目录。

因，这组命令的作用是下载并安装Maven的配置文件，以便在系统中使用Maven构建Java项目。










3.
mvn archetype:generate \
  -DgroupId=shiyanlou.struts \
  -DartifactId=FileUpload  \
  -DarchetypeArtifactId=maven-archetype-webapp
  
  这是一个Maven命令，用于创建一个基于Maven的Struts2文件上传项目。

具体来说，该命令使用了Maven的archetype插件，通过指定不同的参数生成不同类型的项目。其中，该命令使用了maven-archetype-webapp这个archetype，表示生成一个Web应用程序的基本骨。

该命令的具体参数如下：

- archetype:generate：使用archetype插件生成项目。
- -DgroupId=shiyanlou.struts：指定项目的groupId为shiyanlou.struts，即项目的包名。
- -DartifactId=FileUpload：指定项目的artifactId为FileUpload，即项目的名称。
- -DarchetypeArtifactId=maven-archetype-webapp：指定使用maven-archetype-webapp这个archetype来生成项目。

因此，该命令的作用是创建一个基于Maven的Struts2文件上传项目其中包含了Web应用程序的基本骨架。










4.
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>shiyanlou.struts</groupId>
    <artifactId>FileUpload</artifactId>
    <packaging>war</packaging>
    <version>1.0-SNAPSHOT</version>
    <name>FileUpload Maven Webapp</name>
    <dependencies>
        <dependency>
            <groupId>org.apache.struts</groupId>
            <artifactId>struts2-core</artifactId>
            <version>2.5.18</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
            <scope>provided</scope>
        </dependency>

    </dependencies>
    <build>
        <finalName>FileUpload</finalName>
        <plugins>
            <plugin>
                <groupId>org.eclipse.jetty</groupId>
                <artifactId>jetty-maven-plugin</artifactId>
                <version>9.4.12.v20180830</version>
                <configuration>
                    <scanIntervalSeconds>10</scanIntervalSeconds>
                    <webApp>
                        <contextPath>/</contextPath>
                    </webApp>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>

这是一个Maven项目的pom.xml文件，用于配置项目的依赖和构建。

具体来说，该文件包含了以下配置：

- <modelVersion>4.00</modelVersion>：指定POM模型的版本号。
- <groupId>shiyanlou.struts</groupId>：指定项目的groupId，即项目的包名。
- <artifactId>FileUpload</artifactId>：指定项目的artifactId，即项目的名称。
- <packaging>war</packaging>：指定项目的打包方式为war包。
- <version>1.0-SNAPSHOT</version>：指定项目的版本号。
- <name>FileUpload Maven Webapp</name>：指定项目的名称。
- <dependencies>：指定项目的依赖。
- <dependency>：指定一个依赖，其中包含了依赖的groupId、artifactId和version。
- <scope>provided</scope>指定依赖的作用范围为provided，表示该依赖由容器提供。
- <build>：指定项目的构建配置。
- <finalName>FileUpload</finalName>：指定项目构建后的名称。
- <plugins>：指定项目的插件。
- <plugin>：指定一个插件。
- <groupId>org.eclipse.jetty</groupId>：指定插件的groupId。
- <artifactId>jetty-maven-plugin</artifactId>：指定插件的artifactId。
- <version>9.4.12.v20180830</version>：指定插件的版本号。
- <configuration>：指定插件的配置。
- <scanIntervalSeconds>10</scanIntervalSeconds>：指定插件扫描文件的时间间隔。
- <webApp>：指定Web应用程序的配置。
- <contextPath>/</contextPath>：指定Web应用程序的上下文路径为根路径。

因此，该文件的作用是配置Maven项目的依赖和构建，以便在系统中使用Maven构建Java项目。
  
  
  
  
  
  
  
  
  
  
  5.
package shiyanlou.struts;

import java.io.File;

import org.apache.commons.io.FileUtils;
import org.apache.struts2.ServletActionContext;

import com.opensymphony.xwork2.ActionContext;
import com.opensymphony.xwork2.ActionSupport;

public class UploadAction extends ActionSupport {

    private static final long serialVersionUID = 1L;

    // 上传文件者
    private String uploader;
    // 上传的文件
    private File upload;
    // 上传文件类型
    private String uploadContentType;
    // 上传文件的文件名
    private String uploadFileName;
    // 上传文件的保存路径
    private String savePath;

    public String execute() throws Exception{

        // 设置上传文件保存路径
        String realpath = getSavePath();

        // 判断上传文件是否为空
        if (upload != null)  {

            // 根据路径以及文件名，新建一个 File 文件实例
            File savefile = new File(realpath, getUploadFileName());

            // 判断此路径是否已经存在
            if ( !savefile.getParentFile().exists() )
                savefile.getParentFile().mkdirs();

            // 把上传文件拷贝到新路径下，完成上传
            FileUtils.copyFile(upload, savefile);

            // 设置 request 对象值，表示上传成功
            ActionContext.getContext().put("message", "upload succeed!");

            return "success";

        }

         // 其他情况，上传失败
         return "error";

    }

    public String getUploader() {
        return uploader;
    }

    public void setUploader(String uploader) {
        this.uploader = uploader;
    }

    public File getUpload() {
        return upload;
    }

    public void setUpload(File upload) {
        this.upload = upload;
    }

    public String getUploadContentType() {
        return uploadContentType;
    }

    public void setUploadContentType(String uploadContentType) {
        this.uploadContentType = uploadContentType;
    }

    public String getUploadFileName() {
        return uploadFileName;
    }

    public void setUploadFileName(String uploadFileName) {
        this.uploadFileName = uploadFileName;
    }

    public String getSavePath() {

        return ServletActionContext.getServletContext().getRealPath(savePath);
    }

    public void setSavePath(String savePath) {
        this.savePath = savePath;
    }

}
  
  好的，让我来详细分析一下每一句代码。

```java
package shiyanlou.struts;

import java.io.File;

import org.apache.commons.io.FileUtils;
import org.apache.struts2.ServletContext;

import com.opensymphony.xwork2.ActionContext;
import com.opensymphony.xwork2.ActionSupport;

public class UploadAction extends ActionSupport {

    private static final long serialVersionUID = 1L;

    // 上传文件者
    private String uploader;
    // 上传的文件
    private File upload;
    // 上传文件类型
    private String uploadContentType;
    // 上传文件的文件名
    private String uploadFileName;
    // 上传文件的保存路径
    private String savePath;
```

这段代码定义了一个名为 UploadAction 的类，该类继承了 Struts2 框架中的 ActionSupport 类。该类中包含了五个私有属性：uploader、upload、uploadContentType、uploadFileName 和 savePath，分别表示上传文件者、上传的文件、上传文件类型、上传文件的文件名和上传文件的保存路径。

```java
public String execute() throws Exception{

        // 设置上传文件保存路径
        String realpath = getSavePath();

        // 判断上传文件是否为空
        if (upload != null)  {

            // 根据路径以及文件名，新建一个 File 文件实例
            File savefile = new File(realpath, getUploadFileName());

            // 判断此路径是否已经存在
            if ( !savefileFile().exists() )
                savefile.getParentFile().mkdirs();

            // 把上传文件拷贝到新路径下，完成上传
            FileUtils.copyFile(upload, savefile);

            // 设置 request 对象值，表示上传成功
            ActionContext.getContext().put("message", "upload succeed!");

            return "success";

        }

         // 其他情况，上传失败
         return "error";

    }
```

这段代码定义了一个名为 execute 的方法，用于处理文件上传请求。首先，获取上传文件的保存路径，后判断上传文件是否为空。如果上传文件不为空，则根据路径以及文件名，新建一个 File 文件实例，并判断此路径是否已经存在。如果路径不存在，则创建该路径。最后，使用 FileUtils.copyFile() 方法把上传文件拷贝到新路径下，完成上传，并设置 request 对象值，表示成功。如果上传文件为空，则上传失败。

```java
public String getUploader() {
        return uploader;
    }

    public void setUploader(String uploader) {
        this.uploader = uploader;
    }

    public File getUpload() {
        return upload;
    }

    public void setUpload(File upload) {
        this.upload = upload;
    }

    public String getUploadContentType() {
        return uploadContentType;
    }

    public void setUploadContentType(String uploadContentType) {
        this.uploadContentType = uploadContentType;
    }

    public String getUploadFileName() {
        return uploadFileName;
    }

    public void setUploadFileName(String uploadFileName) {
        this.uploadFileName = uploadFileName;
    }

    public String getSavePath() {

        return ServletActionContext.getServletContext().getRealPath(savePath);
    }

    public void setSavePath(String savePath) {
        this.savePath = savePath;
    }
```

这段代码定义了一些 getter 和 setter 方法，用于获取和设置属性值。其中，getSavePath() 方法使用 ServletActionContext 类获取 Servlet 上下文，并返回上传文件的保存路径。

总之，该类实现了文件上传功能，可以通过 Struts2 框架来处理文件上传请求。
  
  
  
  
  
  
  
  
  
  
6.
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE struts PUBLIC
    "-//Apache Software Foundation//DTD Struts Configuration 2.5//EN"
    "http://struts.apache.org/dtds/struts-2.5.dtd">

<struts>
    <constant name="struts.enable.DynamicMethodInvocation" value="true" />
    <package name="shiyanlou.struts" extends="struts-default">
        <default-action-ref name="index" />
        <action name="index" >
            <result name="success">/index.jsp</result>
        </action>
        <action name="upload" class="shiyanlou.struts.UploadAction" method="execute">
            <param name="savePath">/uploadFiles</param>
            <result name="success">/success.jsp</result>
            <result name="error">/error.jsp</result>
        </action>
    </package>
</struts>
  
这是一个 Struts2 配置文件，用于配置 Struts2 框架的行为和处理请求的方式。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
```

这是 文件的声明，指定了 XML 版本和编码方式。

```xml
<!DOCTYPE struts PUBLIC
    "-//Apache Software Foundation//DTD Struts Configuration 2.5//EN"
    "http://struts.apache.org/dtds/struts-2.5.dtd">
```

这是 Struts2 配置文件的 DTD（文档类型定义），用于定义 Struts2 配置文件的结和元素。

```xml
<struts>
```

这是 Struts2 配置文件的根元素，包含了所有的 Struts2 配置信息。

```xml
<constant name="struts.DynamicMethodInvocation" value="true" />
```

这是一个常量配置，用于启用 Struts2 框架的动态方法调用功能。

```xml
<package name="shiyanlou.struts" extends="struts-default">
```

这是一个包配置，用定义 Struts2 应用程序的包结构和命名空间。其中，name 属性指定了包的名称，extends 属性指定了该包继承的父包。

```xml
<default-action-ref name="index" />
```

这是一个默认操作配置，用于指定默认的操作名称。在该配置中，name 属性指定了默认操作的名称为 index。

```xml
< name="index" >
    <result name="success">/index.jsp</result>
</action>
```

这是一个操作配置，用于定义 Struts2 应用程序的操作。其中，name 属性指定了操作的为 index，result 元素指定了操作执行成功后的返回结果为 success，返回的页面为 /index.jsp。

```xml
<action name="upload" class="shiyanlou.struts.UploadAction" method="execute">
    <param name="savePath">/uploadFiles</param>
    <result name="success">/success.jsp</result>
    <result name="error">/error.jsp</result>
</action>
```

这是另一个操作配置，用于处理文件上传请求。其中，name 属性指定了操作的为 upload，class 属性指定了操作对应的处理类为 shiyanlou.struts.UploadAction，method 属性指定了操作对应的处理方法为 execute。param 元素指定了上传文件的保存路径为 /uploadFiles。result 元素指定了操作执行成功后的返回结果为 success，返回的页面为 /success.jsp；指定了操作执行失败后的返回结果为 error，返回的页面为 /error.jsp。

总之，该 Struts2 配置文件定义了 Struts2 应程序的包结构、默认操作、操作和常量等配置信息，用于处理请求和返回结果。
  
  
  
  
  
  
  
  
  
  7.
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Upload Your File</title>
</head>
<body>
    <form action="upload" method="post" enctype="multipart/form-data">
    uploader:<input type="text" name="uploader">
    select file:<input type="file" name="upload">
    <input type="submit" value="Upload">
    </form>
</body>
</html>
 
    这是一个 JSP 页面，用于实现文件上传功能的前端页面。

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
``这是 JSP 页面的声明，指定了页面的编码方式为 UTF-8。

```jsp
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Upload Your File</title>
</head>
<body>
```

这是 HTML 页面的开始标签，包含了页面的头部信息和开始标签。

```jsp
    <form action="upload" method="post" enctype="multipart/form-data">
```

这是一个表单元素，用于提交文件上传请求。其中，action 属性指定了表单提交的地址为 upload，method 属性指了表单提交的方式为 post，enctype 属性指定了表单提交的编码方式为 multipart/form-data。

```jsp
    uploader:<input type="text" name="uploader">
```

这是一个文本输入框，用于输入上传文件的上传者信息。其中，name 属性指定了输入框的名称为 uploader。

```jsp
    select file:<input type="file" name="upload">
```

这是一个文件选择框，用于选择要上传的文件。其中，name 属性指定了选择框的名称为 upload。

```jsp
    <input type="submit" value="Upload">
    </form>
```

这是一个提交按钮，用于提交文件上传请求。其中，value 属性指定了按钮的显示文本为 Upload。

```jsp
</body>
</html>
```

是 HTML 页面的结束标签，用于结束页面的内容。总之，该 JSP 页面实现了文件上传功能的前端页面，包含了上传者信息输入框、文件选择框和提交按钮等元素。
  
  
  
  
  
  
  
  
  
  8.
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib uri="/struts-tags"  prefix="s"%>

<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>File Uploaded</title>
</head>

<body>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

upload succeed!<br/>
uploader:<s:property value=" + uploader"/><br/>
file name:<s:property value="+ uploadFileName"/><br/>
file type:<s:property value="+ uploadContentType"/><br/>
file address:<p> <%=basePath %><s:property value="'uploadFiles/'
    + uploadFileName"/></p><br/>
</body>
</html>
  
  这是一个 JSP 页面，用于显示文件上传成功后的信息。

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
```

这是 JSP 页面的声明，指定了页面的编码方式为 UTF-8。

```
<%@ taglib uri="/struts-tags"  prefix="s"%>
```

这是 Struts2 标签库的引用声明，用于在 JSP 页面中使用 Struts2 的标签。

```jsp
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>File Uploaded</title>
</head>
```

这是 HTML 页面的开始标签，包含了页面的头部信息和开始标签。

```jsp
>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>
```

这是 JSP 页面的 Java 代码块，用于获取上传文件的基本信息。其中，path 变获取了应用程序的上下文路径，basePath 变量获取了应用程序的基本路径。

```jsp
upload succeed!<br/>
uploader:<s:property value=" + uploader"/><br/>
file name:<s:property value="+ uploadFileName"/><br/>
file type:<s:property value="+ uploadContentType"/><br/>
file address:<p> <%=basePath %><s:property value="'uploadFiles/'
    + uploadFileName"/></p><br/>
```

这是 HTML 页面的主体部分，用于显示上传文件的基本信息。其中，uploader、uploadFileName 和 uploadContentType 等变量使用了 Struts2 的标签库，用于获取上传文件的上传者、文件名和文件类型等信息。file address 部分使用了 Java 代码块和 Struts2 标签库，用于获取上传文件的保存地址。

```jsp
</body>
</html>
```

是 HTML 页面的结束标签，用于结束页面的内容。总之该 JSP 页面用于显示文件上传成功后的信息，包含了上传者、文件名、文件类型和文件地址等信息。
  
  
  
  
  
  
  
  
  
  11.
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Upload Error</title>
</head>
<body>
No File selected!
</body>
</html>
    
    这是一个 JSP 页面，用于显示文件上传失败的信息。

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="-8"%>
```

这是 JSP 页面的声明，指定了页面的编码方式为 UTF-8。

```jsp
<!DOCTYPE html>
<html>
<head<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Upload Error</title>
</head>
```

这是 HTML 页面的开始标签，包含了页面的头部信息和开始标签。

jsp
<body>
No File selected!
</body>
```

这是 HTML 页面的主体部分，用于显示文件上传失败的信息。其中，No File selected! 表示没有选择上传文件。

```jsp
</html>
`

是 HTML 页面的结束标签，用于结束页面的内容。总之该 JSP 页面用于显示文件上传失败的信息，提示用户没有选择上传文件。
    
    
    
    
    
    
    
    
    
    
    12.
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         id="WebApp_ID" version="3.0">
  <display-name>FileUpload</display-name>
  <filter>
      <filter-name>struts2</filter-name>
      <filter-class>
        org.apache.struts2.dispatcher.filter.StrutsPrepareAndExecuteFilter
      </filter-class>
   </filter>

   <filter-mapping>
      <filter-name>struts2</filter-name>
      <url-pattern>/*</url-pattern>
   </filter-mapping>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>

</web-app>
    
    这是一个 web.xml 文件，用于配置 Web 应用程序的部署描述符。

```xml
<?xml version="1.0" encoding="UTF-8"?>
```

这是 XML 文件的声明，指定了文件的和编码方式。

```xml
<web-app xmlns:xsi="http://www.w3.org/1/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         id="WebApp_ID" version="3.0">
```

这是 Web 应用程序的根元素，包含了命名空间和版本信息等属性。

```xml
  <display-name>FileUpload</display-name>
```

这是 Web 应用程序的显示名称，于在 Web 服务器中显示。

```xml
  <filter>
      <filter-name>struts2</filter-name>
      <filter-class>
        org.apache.struts2.dispatcher.filter.StrutsPrepareAndExecuteFilter
      </filter-class>
   </filter>

   <filter-mapping>
      <filter-name>struts2</filter-name>
      <url-pattern>/*</url-pattern>
   </filter-mapping>
```

这是 Struts2 框架的过滤器配置，用于拦截所有的请求并进行处理。其中，filter-name 指定了过滤器的名称，filter-class 指定了过滤器的实现类，filter-mapping 指定了过滤器映射规则。

```xml
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>
```

这是 Web 应用程序的欢迎文件列表，用于指定默认的访问页面。其中，welcome-file 指定了欢迎文件的名称，按照顺序依次查找，直到找到可用的文件为止。

```xml
</web-app>
``是 Web 应用程序的结束标签，用于结束文件内容。总之该文件用于配置 Web 应用程序的部署描述符，包含了 Struts2 框架的过滤器配置和欢迎文件列表等信息。
    
    
    
    
    
    
    
    
    
    
    
    13.
mvn jetty:run
    
    这是 Maven 命令，用于启动 Jetty Web 服务器并运行 Web 应用程序。

其中，mvn 是 Maven 命令的前缀，jetty:run 是 Maven Jetty 插件的标，用于启动 Jetty Web 服务器并运行 Web 应用程序。执行该命令后，Maven 会自动下载所需的依赖，并启动 Jetty Web 服务器，然后将 Web 应用程序部署到 Jetty 服务器上并运行。在浏览器中输入 http://localhost:8080 即可访问 Web 应用程序。
    
    
    
    
    
    
    
    
 14.
package shiyanlou.struts;

import java.io.File;
import org.apache.commons.io.FileUtils;
import org.apache.struts2.ServletActionContext;

import com.opensymphony.xwork2.ActionContext;
import com.opensymphony.xwork2.ActionSupport;

public class MultiUploadAction extends ActionSupport {

    private static final long serialVersionUID = 1L;
    private File[] uploads;
    private String[] uploadsContentType;
    private String[] uploadsFileName;
    private String savePath;

    public String execute() throws Exception {
        String realpath = getSavePath();
        if (uploads != null) {
            File savepath = new File(realpath);
            if (!savepath.exists())
                savepath.mkdirs();
            for (int i = 0; i < uploads.length; i++) {

                File savefile = new File(savepath, getUploadsFileName()[i]);

                FileUtils.copyFile(uploads[i], savefile);
            }
            ActionContext.getContext().put("message", "upload succeed!");
            return "success";
        }
        return "error";
    }

    public File[] getUploads() {
        return uploads;
    }

    public void setUploads(File[] uploads) {
        this.uploads = uploads;
    }

    public String[] getUploadsContentType() {
        return uploadsContentType;
    }

    public void setUploadsContentType(String[] uploadsContentType) {
        this.uploadsContentType = uploadsContentType;
    }

    public String[] getUploadsFileName() {
        return uploadsFileName;
    }

    public void setUploadsFileName(String[] uploadsFileName) {
        this.uploadsFileName = uploadsFileName;
    }

    public String getSavePath() {
        return ServletActionContext.getServletContext().getRealPath(savePath);
    }

    public void setSavePath(String savePath) {
        this.savePath = savePath;
    }
}
                                               
这是一个 Struts2 的 Action 类，用于处理多文件上传的请求。

该类继承了 ActionSupport 类，实现了 execute 方法，用于处理上传请求。该类包含了以下属性：

- uploads：上传的文件数组。
-ContentType：上传的文件类型数组。
- uploadsFileName：上传的文件名数组。
- savePath：上传文件保存的路径。

execute 方法首先获取上传文件保存的真实路径，然后遍历上传的文件数组，将每个文件保存到指定的路径中。最后，将上传成功的消息存储到 ActionContext 中，并返回 success 结果。

该类包含了一些 getter 和 setter 方法，用于获取和设置属性值。其中，getSavePath 方法使用 ServletActionContext 获取 Servlet 上下文，并获取上传文件保存的真实路径。

总之，该类用于处理多文件上传的请求，将上传的文件保存到指定的路径中，并返回上传成功的消息。
                                               
                                               
                                               
                                               
                                               
                                               
                                               
                                               
                                               
                                               
15.
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE struts PUBLIC
        "-//Apache Software Foundation//DTD Struts Configuration 2.5//EN"
        "http://struts.apache.org/dtds/struts-2.5.dtd">
<struts>
    <constant name="struts.enable.DynamicMethodInvocation" value="true"/>
    <package name="shiyanlou.struts" extends="struts-default">
        <default-action-ref name="index"/>
        <action name="index">
            <result name="success">/index.jsp</result>
        </action>
        <action name="multiUpload" class="shiyanlou.struts.MultiUploadAction"
                method="execute">
            <interceptor-ref name="fileUpload">
                <param name="allowedTypes">text/plain,image/png,image/gif,image/jpeg</param>
                <param name="maximumSize">20480</param>
            </interceptor-ref>
            <interceptor-ref name="defaultStack"></interceptor-ref>
            <param name="savePath">/uploadMultiFiles</param>
            <result name="success">/success.jsp</result>
            <result name="error">/error.jsp</result>
            <result name="input">/index.jsp</result>
        </action>
    </package>
</struts>
  

1. `<?xml version="1.0" encoding="UTF-8" ?>`：这是 XML 声明，指定了使用的 XML 版本文件的字符编码。

2. `<!DOCTYPE struts PUBLIC "-//Apache Software Foundation//DTD Struts Configuration 2.5//EN" "http://struts.apache.org/dtds/struts-2.5.dtd">`：这是 DOCTYPE 声明，指定了 Struts 配置文件的 DTD（文档类型定义）。

3. `<struts>`：这是 Struts 配置文件的根元素。

4. `<constant name="struts.enable.DynamicMethodInvocation" value="true"/>`：这一行定义了一个常量，启用了 Struts2 中的动态方法调用。

5. `<package name="shiyanlou.struts" extends="struts-default">`：这一行定义了一个名为 "shiyanlou.struts" 的包，继承了默认的 Struts2 包。

6. `<default-action-ref name="index"/>`：这一行将默认的 Action 设置为 "index"。

7. `<action name="index">`：这一行定义了一个名为 "index" 的 Action。

8. `<result name="success">/index.jsp</result>`：这一行定义了一个名为 "success" 的结果，映射到 JSP 页面 "/index.jsp"。

9. `</action>`：这一行结束了 "index" Action。

10. `<action name="multiUpload" class="shiyanlou.struts.MultiUploadAction" method="execute">`：这一行定义了一个名为 "multiUpload" 的 Action，使用 "MultiUploadAction" 类处理请求，使用 "execute" 方法处理请求。

11. `<interceptor-ref name="fileUpload">`：这一行将 "fileUpload" 拦截器添加到 Action 中，用于处理文件上传。

12. `<param name="allowedTypes">text/plain,image/png,image/gif,image/jpeg</param>`：这一行设置了文件上传的允许类型。

13. `<param name="maximumSize">20480</param>`：这一行设置了文件上传的最大大小。

14. `</interceptor-ref>`：这一行结束了 "fileUpload" 拦截器。

15. `<interceptor-ref name="defaultStack"></interceptor-ref>`：这一行将默认的拦截器栈添加到 Action 中。

16. `<param name="savePath">/uploadMultiFiles</param>`：这一行设置了上传文件保存的路径。

17. `<result name="success">/success.jsp</result>`：这一行定义了一个名为 "success" 的结果，映射到 JSP 页面 "/success.jsp"。

18. `<result name="error">/error.jsp</result>`：这一行定义了一个名为 "error" 的结果，映射到 JSP 页面 "/error.jsp"。

19. `<result name="input">/index.jsp</result>`：这一行定义了一个名为 "input" 的结果，映射到 JSP 页面 "/index.jsp"。

20. `</action>`：这一行结束了 "multiUpload" Action。

21. `</package>`：这一行结束了 "shiyanlou.struts" 包。

22. `</struts>`：这一行结束了 Struts 配置文件的根元素。

总的来说，这个 Struts2 配置文件定义了两个 Action： "index" 和 "multiUpload"。 "index" 简单地返回 "/index.jsp" 页面，而 "multiUpload" Action 处理文件上传并根据上传结果返回 "/success.jsp"、"/error.jsp" 或 "/index.jsp" 页面。
  
  
  
  
  
  
  
  
  
  
  16.
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib uri="/struts-tags"  prefix="s"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Upload Your File</title>
</head>
<body>
<s:form action="multiUpload" method="post" enctype="multipart/form-data">
<s:file label="select file1" name="uploads" />
<s:file label="select file2" name="uploads" />
<s:file label="select file3" name="uploads" />
<s:submit value="Upload" />
</s:form>
</body>
</html>
  
  这是一个 JSP 页面，用于上传多个文件。让我解释一下其中的每一行代码：

1. `<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>`：这是 J 页面的指令，指定了页面使用的编程语言、内容类型和字符编码。

2. `<%@ taglib uri="/struts-tags"  prefix="s"%>`：这是 JSP 页面的指令，引入了 Struts2 标签库，使页面可以使用 Struts2 的标签。

3. `<!DOCTYPE html>`：这是 HTML5 的 DOCTYPE 声明。

4. `<html>`：这是 HTML 页面的根元素。

5. `<head>`：这是 HTML 页面的头部，包含了页面的元数据。

6. `<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">`：这是 HTML 页面的元数据，指定了页面的内容类型和字符编码。

. `<title>Upload Your File</title>`：这是 HTML 页面的标题，显示在浏览器的标签页上。

8. `</head>`：头部结束标签。

9. `<body>`：这是 HTML 页面的主体，包含页面的内容。

10. `<s:form action="multiUpload" method="post" enctype="multipart/form-data">`：这是 Struts2 的表单标签，定义了一个名为 "multiUpload" 的 Action，使用 POST 方法提交表单，enctype 属性指定了表单数据的编码类型为 multipart/form-data11. `<s:file label="select file1" name="uploads" />`：这是 Struts2 的文件上传标签，定义了一个文件上传控件，label 属性指定了控件的标签文本，name 属性指定控件的名称。

12. `<s:file label="select file2" name="uploads" />`：同上，定义了第二个文件上传控件。

13. `<s:file label="select file3" name="uploads" />`：同上，定义了第三个文件上传控件。

14. `<s:submit value="" />`：这是 Struts2 的提交按钮标签，定义了一个提交按钮，value 属性指定了按钮的文本。

15. `</s:form>`：表单结束标签。

16. `</body>`：主体结束标签。

17 `</html>`：HTML 页面结束标签。

总的来说，这个 JSP 页面使用了 Struts2 的标签库，定义了一个包含三个文件上传控件和一个提交按钮的表单，用于上传多个文件。表单提交后将会调用名为 "multiUpload" 的 Action 处理上传的文件。
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
17.
<body>
  <%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<h1>upload succeed!</h1><br/>

file name:<s:property value="+ uploadsFileName[0]"/><br/>
file type:<s:property value="+ uploadsContentType[0]"/><br/>
file address:<p> <%=basePath %><s:property value="'uploadMultiFiles/'
        + uploadsFileName[0]"/></p><br/>

file name:<s:property value="+ uploadsFileName[1]"/><br/>
file type:<s:property value="+ uploadsContentType[1]"/><br/>
file address:<p> <%=basePath %><s:property value="'uploadMultiFiles/'
        + uploadsFileName[1]"/></p><br/>

file name:<s:property value="+ uploadsFileName[2]"/><br/>
file type:<s:property value="+ uploadsContentType[2]"/><br/>
file address:<p> <%=basePath %><s:property value="'uploadMultiFiles/'
        + uploadsFileName[2]"/></p><br/>

  </body>
    
    这是一个 JSP 页面，用于在上传多个文件后显示上传成功的信息。让我解释一下其中的每一行代码：

1. `<%` 和 `%>`：这是 JSP 页面的脚本标记，用于嵌入 Java 代码。

2. `String path = request.getContextPath();`：获取当前应用程序的上下文路径。

3. `String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";`：获取当前应用程序的基本 URL，包括协议、主机名、端口和上下文路径。

4. `<h1>upload succeed!</h1><br/>`：显示上传成功的信息。

5. `file name:<s:property value="+ uploadsFileName[0]"/><br/>`：显示第一个上传文件的文件名。

6. `file type:<s:property value="+ uploadsContentType[0]"/><br/>`：第一个上传文件的文件类型。

7. `file address:<p> <%=basePath %><s:property value="'uploadMultiFiles/'
        + uploadsFileName[0]"/></p><br/>`：显示第一个上传文件的文件地址，其中 <%=basePath %> 表示基本 URL，<s:property value="'uploadMultiFiles/' + uploadsFileName[0]" /> 表示上传文件的相对路径。

8. `file name:<s:property="+ uploadsFileName[1]"/><br/>`：同上，显示第二个上传文件的文件名。

9. `file type:<s:property value="+ uploadsContentType[1]"/><br/>`：同上，显示第二个上传文件的文件类型。

10. `file address:<p> <%=basePath %><s:property value="'uploadMultiFiles/'
        + uploadsFileName[1]"/></p><br/>`：同上，显示第二个上传文件的文件地址。

11. `file name:<s:property value="+ uploadsFileName[2]"/><br/>`：同上，显示第三个上传文件的文件名。

12. `file type:<s:property value="+ uploadsContentType[2]"/><br/>`：同上，显示第三个上传文件的文件类型。

13. `file address:<p> <%=basePath %><s:property value="'uploadMultiFiles/'
        + uploadsFileName[2]"/></p><br/>`：同上，显示第三个上传文件的文件地址。

总的来说这个 JSP 页面使用了 Struts2 的标签库，显示了上传成功的信息，包括每个上传文件的文件名、文件类型和文件地址。其中，文件地址使用了当前应用程序的基本 URL 和上传文件的相对路径。
    
    
    
    
    
    
    
    
    
    
    18.
mvn jetty:run
    
    这是 Maven 命令，用于启动 Jetty Web 服务器。让我解释一下其中的每一个部分：

1. `mvn`：这是 Maven 命令的前缀，于执行 Maven 命令。

2. `jetty:run`：这是 Maven Jetty 插件的目标，用于动 Jetty Web 服务器并运 Web 应用程序。

当你在命令行中输入 `mvn jetty:run` 后，Maven 将会执行 Jetty 插件的 run 目标，启动 Jetty Web 服务器并运行 Web 应用程序。在执行此命令之前，你需要确保已经在项目的根录下运行了 `mvn clean install` 命令，以确保项目已经被编译、打包并安装到本地 Maven 仓库中。
