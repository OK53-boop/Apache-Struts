1.
package shiyanlou.struts;

import java.io.FileNotFoundException;
import java.io.InputStream;

import org.apache.struts2.ServletActionContext;

import com.opensymphony.xwork2.ActionSupport;

public class DownloadAction extends ActionSupport {


    /**
     *
     */
    private static final long serialVersionUID = 1L;

    // 下载路径
    private String downloadPath;

    // 下载文件的文件名
    private String filename;

    public String getFilename() {
           return filename;
    }

    public void setFilename(String filename) {
           this.filename = filename;
    }

    public void setDownloadPath(String downloadPath){
           this.downloadPath = downloadPath;
    }

public InputStream getTargetFile() throws FileNotFoundException
{
    // 获得下载文件的真实路径
    String realPath = downloadPath + "/" + getFilename();

    // 返回下载文件对应的输入流
    return ServletActionContext.getServletContext().getResourceAsStream(realPath);
}

public String execute()
{
    return "success";
}

}


这是一个 Struts2 的 Action 类，用于实现文件下载功能。让我解释一下其中的每一个部分：

1. `package shiyanlou;`：声明了该类所在的包。

2. `import`：导入所需的类。

3. `public class DownloadAction extends ActionSupport`：定义了一个名 DownloadAction 的公共类，继承自 Struts2 的 ActionSupport 类。

4. `private String downloadPath;`：定义了一个私有的字符串类型变量 downloadPath，用于存储下载文件的路径。

5. `private String filename;`：定义了一个私有的字符串类型变量 filename，用于存储下载文件的文件名。

6. `public String getFilename() {...}` 和 `public void setFilename(String filename) {...}`：定义了获取和设置 filename 变量的方法。

7 `public void setDownloadPath(String downloadPath) {...}`：定义了设置 downloadPath 变量的方法。

8. `public InputStream getTargetFile() throws FileNotFoundException {...}`：定义了获取下载文件输入流的方法。该方法首先获取下载文件的真实路径，然后返回该文件对应的输入流。

9. `public String execute() {...}`：定义了执行下载操作的方法。该方法返回字符串类型的 "success，表示下载操作执行成功。

总的来说，这个 Action 类实现了文件下载功能，通过获取下载文件的真实路径和返回该文件对应的输入流来实现文件下载。












2.
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
    <package name="shiyanlou.struts.download" extends="struts-default">
  <action name="download" class="shiyanlou.struts.DownloadAction" method="execute">

     <param name="downloadPath">/uploadMultiFiles</param>

        <result name="success" type="stream">

           <param name="inputName">targetFile</param>

          <!-- <param name="contentType">image/jpg</param> -->

           <param name="contentDisposition">attachment;filename=${filename}</param>

           <param name="bufferSize">4096</param>
      </result>
   </action>
 </package>
</struts>

这是一个 Struts2 的配置文件，用于配置应用程序的行为。让我解释一下其中的每一个部分：

1. `<?xml version="1.0" encoding="UTF-8" ?>`：声明了该文件的 XML 版本和码方式。

2. `<!DOCTYPE struts PUBLIC "-//Apache Software Foundation//DTD Struts Configuration 2.5//EN" "http://struts.apache.org/dtds/struts-2.5.dtd">`：声明了该文件的 DTD（文档类型定义）。

3. `<struts>`：定义了 Struts2 的配置文件的根元素。

4. `<constant name="struts.enable.DynamicMethodInvocation" value="true"/>`：定义了一个常量，用于启用动态方法调用。

5. `<package name="shiyanlou.struts" extends="struts-default">`：定义了一个名为 shiyanlou.struts 的包，继承自 Struts2 默认包。

6. `<default-action-ref name="index"/>`：定义了默认的 Action，当请求的 Action 不存在时，将会使用该 Action7. `<action name="index">...</action>`：定义了一个名为 index 的 Action，用于显示主页。

8. `<action name="multiUpload" class="shiyanlou.struts.MultiUploadAction" method="execute">...</action>`：定义了一个名为 multiUpload 的 Action，使用 MultiUploadAction 类处理请求，并调用 execute 方法。

9. `<interceptor-ref name="fileUpload">...</interceptor-ref>`：定义了一个名为 fileUpload 的拦截器，用于处理文件上传操作。

10. `<param name="allowedTypes">text/plain,image/png,image/gif,image/jpeg</param>`：定义了允许上传的文件类型。

11. `<param name="maximumSize">20480</param>`：定义了上传文件的最大大小，单位为字节。

12. `<param name="savePath">/uploadMultiFiles</param>`：定义了上传文件的保存路径。

13. `<result name="success">...</result>`：定义了 Action 执行成功时的返回结果。

14. `<result name="error">...</result>`：定义了 Action 执行失败时的返回结果。

15. `<result name="input">...</result>`：定义了 Action 输入验证失败时的返回结果。

16. `<package name="shiyanlou.struts.download" extends="struts-default">...</package>`：定义了一个名为 shiyanlou.struts.download 的包，继承自 Struts2 默认包。

17. `<action name="download" class="shiyanlou.struts.DownloadAction" method="execute">...</action>`：定义了一个名为 download 的 Action，使用 DownloadAction 类处理请求，并调用 execute 方法。

18 `<param name="downloadPath">/uploadMultiFiles</param>`：定义了下载文件的路径。

19. `<result name="success" type="stream">...</result>`：定义了 Action 执行成功时的返回结果，使用流的方式返回下载文件。









3.
<body>
  <%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<h1>upload succeed!</h1><br/>

file name:<s:property value="+ uploadsFileName[0]"/><br/>
file type:<s:property value="+ uploadsContentType[0]"/><br/>
file address:  <%=basePath %><s:property value="'uploadMultiFiles/'
        + uploadsFileName[0]"/>  <a href="download.action?filename=<s:property value="+ uploadsFileName[0]"/>">download</a> <br/>
 <br/>
file name:<s:property value="+ uploadsFileName[1]"/><br/>
file type:<s:property value="+ uploadsContentType[1]"/><br/>
file address: <%=basePath %><s:property value="'uploadMultiFiles/'
        + uploadsFileName[1]"/> <a href="download.action?filename=<s:property value="+ uploadsFileName[1]"/>">download</a> <br/>
 <br/>
 <br/>
file name:<s:property value="+ uploadsFileName[2]"/><br/>
file type:<s:property value="+ uploadsContentType[2]"/><br/>
file address: <%=basePath %><s:property value="'uploadMultiFiles/'
        + uploadsFileName[2]"/>  <a href="download.action?filename=<s:property value="+ uploadsFileName[2]"/>">download</a> <br/>

  </body>
    
这是一个 JSP 页面，用于显示上传文件的信息和下载链接。让我解释一下其中的每一个部分：

1. `<% ... %>`：这 JSP 中的脚本片段，用于在页面中嵌入 Java 代码。

2. `String path = request.getContextPath();`：获取应用程序的上下文路径。

3. `String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";`：获取应用程序的基础 URL。

4. `<h1>upload succeed!</h1><br/>`：显示上传成功的提示。

5. `<s:property value="+ uploadsFileName[0]"/>`：使用 Struts2 标签库的 `<s:property>` 标签，显示上传文件的文件名。

6. `<s:property value="+ uploadsContentType[0]`：使用 Struts2 标签库的 `<s:property>` 标签，显示上传文件的文件类型。

7. `<%=basePath %>`：使用 Java 代码，显示应用程序的基础 URL。

8. `<s:property value="'uploadMultiFiles/' + uploadsFileName[0]`：使用 Struts2 标签库的 `<s:property>` 标签，显示上传文件的保存路径。

9. `<a href="download.action?filename=<s:property value="+ uploadsFileName[0]"/>">download</a>`：显示下载链接，链接到下载 Action，并传递文件名参数。

10. 类似的，使用上述方式显示第二个和第三个上传文件的信息和下载链接。









