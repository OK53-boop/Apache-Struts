1.
FormValidate
├── pom.xml
└── src
    └── main
        ├── java
        │   └── shiyanlou
        ├── resources
        │   └── structs.xml
        └── webapp
            ├── register.jsp
            ├── success.jsp
            └── WEB-INF
                └── web.xml

这是一个 Maven 项目的目录结构，其中包含了一个名为 "FormValidate" 的 Web 应用程序。下面是对每个目录和文件的详细分析：

1 `pom.xml`：Maven 项目的配置文件，用于定义项目的依赖项和构建设置。

2. `src`：源代码目录3. `main`：主目录，包含应用程序的主要代码和资源。

4. `java`：Java 代码目录，包含应用程序的 Java 类文件。

5. `shiyanlou`：Java 包名，包含应用程序的 Java 类文件。

6. `resources`：资源目录，包含应用程序的配置文件和其他资源文件。

7. `structs.xml`Struts2 框架的配置文件，用于配置应用程序的控制器和视图。

8. `webapp`：Web 应用程序目录，包含应用程序的 Web 资源文件。

9. `register.jsp`：应用程序的注册页面，用于收集用户信息10. `success.jsp`：应用程序的成功页面，用于显示用户注册成功的消息。

11. `WEB-INF`：Web 应用程序的配置目录。

12. `web.xml`：Web 应用程序的配置文件，用于配置应用程序的过滤器和欢迎页面。

总体来说，这个目录结构是一个标准的 Maven Web 应用程序目录结构，其中包了一个使用 Struts2 框架实现的用户注册功能。该应用程序的 Java 代码位于 `shiyanlou` 包中，注册页面和成功页面位于 `webapp` 目录中，应用程序的配置文件位于 `resources` 和 `WEB-INF` 目录中。













2.
FormValidate/src/main/java/shiyanlou
└── structs
    └── form
        └── vali
            ├── User.java
            ├── ValidateAction.java
            └── ValidateAction-validation.xml
            
这是一个 Java 包的目录结构，其中包含了一个名为 "User" 的 Java 类和一个名为 "ValidateAction" 的 Struts2 控制器类，以及一个名为 "ValidateAction-validation.xml" 的 Struts2 验证配置文件。下是对每个文件的详细分析：

1. `User.java`：一个 Java 类，用于表示用户对象。该类包含了用户的姓名、子邮件和密码等属性，以及相应的 getter 和 setter 方法。

2. `ValidateAction.java`：一个 Struts2 控制器类，用于处理用户注册请求。该类包含了一个名为 "execute" 的方法，该方法处理用户提交的表单数据，并将其保存到数据库中。该类还包含了一些验证逻辑，以确保用户输入的数据有效。

3. `ValidateAction-validation.xml`：一个 Struts2 验证配置文件，用于定义表单字段的验证规则。该文件包含了一些验证规则，例如必字段、电子邮件格式验证和密码长度验证等。

总体来说，这个目录结构是一个标准的 Java 包目录结构，其中包含了一个用于用户注册的 Struts2 控制器类和一个用于表示用户对象的 Java 类。此外，还有一个 Struts2 验证配置文件，用于定义表单的验证规则。











3.
mvn archetype:generate \
  -DgroupId=shiyanlou \
  -DartifactId=FormValidate  \
  -DarchetypeArtifactId=maven-archetype-webapp
  
  这是一个 Maven 命令，用于生成一个名为 "FormValidate" 的 Web 应用程序项目。下面是对每个参数的详细解释1. `mvn archetype:generate`：使用 Maven 的 Archetype 插件生成项目。

2. `-DgroupId=shiyanlou`：指定项目的 Group 为 "shiyanlou"，这是一个唯一标识符，用于区分不同的项目。

3. `-DartifactId=FormValidate`：指定项目的 Artifact ID 为 "FormValidate"，这是项目的名称。

4. `-DarchetypeArtifactId=maven-archetype-webapp`指定使用 "maven-archetype-webapp" Archetype，这是一个标准的 Maven Web 应用程序 Archetype，用于生成一个基本的 Web 应用程序项目。

总体来说，这个命令是用于生成一个基本的 Maven Web 应用程序项目的，其中包含了一个标准的 Maven 目录结构和一些基本的配置文件。该项目可以用于开发 Web 应用程序，并可以根据需要进行自定义和扩展。











4.
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>shiyanlou</groupId>
    <artifactId>FormValidate</artifactId>
    <packaging>war</packaging>
    <version>1.0-SNAPSHOT</version>
    <name>FormValidate Maven Webapp</name>
    <dependencies>
        <dependency>
            <groupId>org.apache.struts</groupId>
            <artifactId>struts2-core</artifactId>
            <version>2.5.18</version>
        </dependency>
    </dependencies>
    <build>
        <finalName>FormValidate</finalName>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**.*</include>
                </includes>
            </resource>
        </resources>
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

这是一个 Maven POM 文件，用于配置 "FormValidate" Web 应用程序项目。下面是对每个元素的详细解释：

1. `<project>`：根元素用于定义 Maven 项目。

2. `<modelVersion>`：指定 POM 模型的版本，通常为 "4.0.0"。

3. `<>`：指定项目的 Group ID，这是一个唯一标识符，用于区分不同的项目。

4. `<artifactId>`：指定项目的 Artifact ID，这是项目的名称。

5. `<packaging>`：指定项目的打包方式，通常为 "war"。

6. `<version>`：指定项目的版本号，通常为 "10-SNAPSHOT"。

7. `<name>`：指定项目的名称。

8. `<dependencies>`：用于定义项目的依赖项。

9. `<dependency>`：用于定义一个依赖项。

10. `<groupId>`：指定依赖项的 Group ID。

11. `<artifactId>`：指定依赖项的 Artifact ID。

12. `<version>`：指定依赖项的版本号。

13. `<build>`：用于定义项目的构建配置。

14. `<finalName>`：指定项目构建后的名称。

15. `<resources>`：用于定义项目的资源目录。

. `<resource>`：用于定义一个资源目录。

17. `<directory>`：指定资源目录的路径。

18. `<includes>`：用于指定包含的文件。

19. `<include>`：用于指定包含的文件名。

20. `<plugins>`：用于定义项目的插件。

21. `<plugin>`：用于定义一个插件。

22. `<groupId>`：指定插件的 Group ID。

23. `<artifactId>`：指定插件的 Artifact ID。

24. `<version>`：指定插件的版本号。

25. `<configuration>`：用于配置插件。

26. `<scanIntervalSeconds>`：指定 Jetty 插件扫描文件的时间间隔。

27. `<webApp>`：用于配置 Web 应用程序。

28. `<contextPath>`：指定 Web 应用程序的上下文路径。

总体来说，这个 POM 文件是用于配置 "FormValidate" Web 应用程序项目的，其中包含了 Struts2 和 Jetty 插件的依赖项和配置。该文件还定义了项目的资源目录和构建配置，以及 Web 应用程序的上下文路径。














5.
package shiyanlou.struts.form.vali;

public class User {

    private String name;
    private String password;
    private String confirmPassword;
    private int age;
    private String mobile;
    private String email;

    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getPassword() {
        return password;
    }
    public void setPassword(String password) {
        this.password = password;
    }
    public String getConfirmPassword() {
        return confirmPassword;
    }
    public void setConfirmPassword(String confirmPassword) {
        this.confirmPassword = confirmPassword;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
    public String getMobile() {
        return mobile;
    }
    public void setMobile(String mobile) {
        this.mobile = mobile;
    }
    public String getEmail() {
        return email;
    }
    public void setEmail(String email) {
        this.email = email;
    }

    @Override
    public String toString() {
        return "User： name=" + name + ", password=" + password
                + ", confirm password=" + confirmPassword + ", age=" + age
                + ", mobile=" + mobile + ", email=" + email ;
    }
}

这是一个 Java 类，名为 User，用于表示用户对象。下面是对每一句代码的详细分析：

1. `package shiyanlou.struts.form.vali;`：定义了 User 类所在包名。

2. `public class User {`：定义了 User 类，它是一个公共类，可以被其他类访问。

3. `private String name`：定义了一个私有的字符串类型变量 name，用于存储用户的姓名。

4. `private String password;`：定义了一个私有的字符串类型变量 password，用于存储用户的密码。

5. `private String confirmPassword;`：定义了一个私有的字符串类型变量 confirmPassword，用于存储用户确认的密码。

6. `private int age;`：定义了一个私有的整型变量 age，用于存储用户的年龄。

7.private String mobile;`：定义了一个私有的字符串类型变量 mobile，用于存储用户的手机号码。

8. `private String email;`：定义了一个私有的字符串类型变量 email，用于存储用户的电子邮件地址。

9. `public String getName() {`：定义了一个公共的方法 getName，用于获取用户的姓名。

10. ` name;`：返回用户的姓名。

11. `public void setName(String name) {`：定义了一个公共的方法 setName，用于设置用户的姓名。

12. `this.name = name;`：将传入的参数 name 赋值给变 name。

13. `public String getPassword() {`：定义了一个公共的方法 getPassword，用于获取用户的密码。

14. `return password;`：返回用户的密码。

15. `public void setPassword(String password) {`：定义了一个公共的方法 setPassword，用于设置用户的。

16. `this.password = password;`：将传入的参数 password 赋值给变量 password。

17. `public String getConfirmPassword() {`：定义了一个公共的方法 getConfirmPassword，用获取用户确认的密码。

18. `return confirmPassword;`：返回用户确认的密码。

19. `public void setConfirmPassword(String confirmPassword) {`：定义了一个公共的方法 setConfirmPassword，用于设置用户确认的密码。

20. `this.confirmPassword = confirmPassword;`：将传入的参数 confirmPassword 赋值给变量 confirmPassword。

21. `public int getAge() {`：定义了一个公共的方法 getAge，用于获取用户的年龄。

22. `return age;`：返回用户的年龄23. `public void setAge(int age) {`：定义了一个公共的方法 setAge，用于设置用户的年龄。

24. `this.age = age;`：将传入的参数 age 赋值给变量 age。

25. `public String getMobile() {`：定义了一个公共的方法 getMobile，用于获取用户的手机号码。

26. `return mobile;`：返回用户的手机号码。

27. `public void setMobile(String mobile) {`：定义了一个公共的方法 setMobile，用于用户的手机号码。

28. `this.mobile = mobile;`：将传入的参数 mobile 赋值给变量 mobile。

29. `public String getEmail() {`：定义了一个公共的方法 getEmail，用于获取用户的电子邮件地址。

30. ` email;`：返回用户的电子邮件地址。

31. `public void setEmail(String email) {`：定义了一个公共的方法 setEmail，用于设置用户的电子邮件地址。

32. `this.email = email;`：将传入的参数 email 赋值给变量 email。

33. `@Override`：表示该是覆盖了父类的方法。

34. `public String toString() {`：定义了一个公共的方法 toString，用于将 User 对象转换为字符串。

35. `return "User： name=" + name + ", password=" + password`返回一个字符串，包含用户的姓名和密码。

36. `+ ", confirm password=" + confirmPassword + ", age=" + age`：将用户的确认密码和年龄添加到字符串中。

37. `+ ", mobile=" + mobile + ", email=" + email ;`：将用户的手机号码和电子邮件地址添加到字符串中，并以分号结尾。














6.
package shiyanlou.struts.form.vali;

import com.opensymphony.xwork2.ActionSupport;

public class ValidateAction extends ActionSupport {

    private static final long serialVersionUID = 1L;

    private User user;

    public User getUser() {
        return user;
    }
    public void setUser(User user) {
        this.user = user;
    }

    public String execute() {
        return "success";
    }

}

这是一个 Java 类，名为 ValidateAction，用于处理用户提交的表单数据。下面是对每一句代码的详细分析：

1. `package shiyanlou.struts.form.val;`：定义了 ValidateAction 类所在包名。

2. `import com.opensymphony.xwork2.ActionSupport;`：导入 com.opensymphony.xwork2.ActionSupport 类，该类是 Struts2 框架中的一个基础类，提供了一些常用的方法和属性。

3. `public class ValidateAction extends ActionSupport {`：定义了 ValidateAction 类，它继承了 ActionSupport 类，表示 ValidateAction 类是一个 Struts2 的 Action 类。

4. `private static final long serialVersionUID = 1L;`：定义了一个私有的静态常量 serialVersionUID，用于序列化反序列化对象。

5. `private User user;`：定义了一个私有的 User 类型变量 user，用于存储用户提交的表单数据。

6. `public User getUser() {`：定义了一个公共的方法 getUser，用获取用户提交的表单数据。

7. `return user;`：返回用户提交的表单数据。

8. `public void setUser(User user) {`：定义了一个公共的方法 setUser，用于设置用户提交的表单数据。

9. `this.user = user;`：将传入的参数 user 赋值给变量 user。

10. `public String execute() {`：定义了一个公共的方法 execute，用于处理用户提交的表单数据。

11. `return "success";`：返回一个字符串 "success"，表示处理成功。










7.
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE struts PUBLIC
        "-//Apache Software Foundation//DTD Struts Configuration 2.5//EN"
        "http://struts.apache.org/dtds/struts-2.5.dtd">
<struts>

    <package name="shiyanlou.struts.form.vali" extends="struts-default">
        <default-action-ref name="index" />
        <action name="index" >
            <result name="success">/register.jsp</result>
        </action>
        <action name="register" class="shiyanlou.struts.form.vali.ValidateAction" method="execute">
            <result name="success">/success.jsp</result>
            <result name="input">/register.jsp</result>
        </action>
    </package>

</struts>

这是一个 Struts2 的配置文件，名为 struts.xml，用于配置应用程序的行为。下面是对每一句代码的详细分析：

1. `<?xml version="1." encoding="UTF-8" ?>`：XML 声明，指定了 XML 版本和编码方式。

2. `<!DOCTYPE struts PUBLIC "-//Apache Software FoundationDTD Struts Configuration 2.5//EN" "http://struts.apache.org/dtds/struts-2.5.dtd">`：DOCTYPE 声明，指定了 Struts2 配置文件的 DTD。

3. `<struts：Struts2 配置文件的根元素。

4. `<package name="shiyanlou.struts.form.vali" extends="struts-default">`：定义了一个名为 shiyanlou.struts.form.vali 的包，它继承了 struts-default 包，表示该包中的 类可以使用 struts-default 包中的配置。

5. `<default-action-ref name="index" />`：定义了默认的 Action，当用户访问应用程序的根目录时，将自动跳转到名为 index 的 Action。

6 `<action name="index" >`：定义了一个名为 index 的 Action。

7. `<result name="success">/register.jsp</result>`：定义了一个名为 success 的结果，表示当 Action 执行成功时，将跳转到 register.jsp 页面。

8. `</action>`：结束 index Action 的定义。

9. `<action name="register" class="shiyanlou.struts.form.vali.ValidateAction" method="execute">`：定义了一个名为 register 的 Action，它使用 ValidateAction 类处理用户提交的表单数据。

10. `<result name="success">/success.jsp</result>`：定义了一个名为 success 的结果，表示当 Action 执行成功时，将跳转到 success.jsp 页面。

11. `<result name="input">/register.jsp</result>`：定义了一个名为 input 的结果，表示当用户提交的表单数据不合法时，将跳转到 register.jsp 页面。

12. `</action>`：结束 register Action 的定义。

13. `</package>`：结束 shiyanlou.struts.form.vali 包的定义。

14. `</struts>`：Struts2 配置文件的结束标签。









8.
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib uri="/struts-tags" prefix="s" %>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
<h2>Type your information to register.</h2>

    <s:fielderror />
    <s:form action="register" method="post">
        <s:textfield label="username" name="user.name" tooltip="name must be over 3 characters"></s:textfield>
        <s:textfield type="password" label="password" name="user.password" tooltip="password must over 6 digits"></s:textfield>
        <s:textfield type="password" label="confirm password" name="user.confirmPassword"></s:textfield>
        <s:textfield label="age" name="user.age" tooltip="age must over 16"></s:textfield>
        <s:textfield label="mobile" name="user.mobile" tooltip="input correct mobile phone number format"></s:textfield>
        <s:textfield label="email" name="user.email" tooltip="input correct email format"></s:textfield>

        <s:submit label="Register"></s:submit>
   </s:form>

</body>
</html>

这是一个 JSP 页面，名为 register.jsp，用于显示用户注册表单。下面是对每一句代码的详细分析：

1. `<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF8"%>`：JSP 页面的指令，指定了页面的编码方式为 UTF-8。

2. `<%@ taglib uri="/struts-tags" prefix="s" %>`：JSP 页面的指令，导入了 Struts2 的标签库，使得页面可以使用 Struts2 的标签。

3. `<!DOCTYPE html>`HTML5 的文档类型声明。

4. `<html>`：HTML 页面的根元素。

5. `<head>`：HTML 页面的头部元素，用于定义页面的元数据。

6. `<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">`：定义了页面的编码方式为-8。

7. `<title>Insert title here</title>`：定义了页面的标题。

8. `</head>`：头部元素的结束标签。

9. `<body>`：HTML 页面的主体元素。

10. `<h2>Type your information to register.</h>`：页面的标题，用于提示用户输入信息。

11. `<s:fielderror />`：Struts2 的标签，用于显示表单验证错误信息。

12. `<s:form action="register" method="post">`：Struts2 的标签，定义了一个表单，它的 属性指定了表单提交的地址，method 属性指定了表单提交的方式为 POST。

13. `<s:textfield label="username" name="user.name" tooltip="name must be over 3 characters"></s:textfield>`：Struts2 的标签，定义了一个文本框，它的 label 属性指定了文本框的标签名，name 属性指定了文本框的名称，tooltip 属性指定了文本框的提示信息。

14. `<s:textfield type="password" label="password" name="user.password" tooltip="password must over 6 digits"></s:textfield>`：Struts2 的标签，定义了一个密码框，它的 label 属性指定了密码框的标签名，name 属性指定了密码框的名称，tooltip 属性指定了密码框的提示信息15. `<s:textfield type="password" label="confirm password" name="user.confirmPassword"></s:textfield>`：Struts2 的标签，定义了一个确认密码框，它的 label 属性指定了确认密码框的标签名，name 属性指定了确认密码框的名称。

16. `<s:textfield label="age" name="user.age" tooltip="age must over 16"></s:textfield>`：Struts2 的标签，定义了一个年龄框，它的 label 属性指定了年框的标签名，name 属性指定了年龄框的名称，tooltip 属性指定了年龄框的提示信息。

17. `<s:textfield label="mobile" name="user.mobile" tooltip="input correct mobile phone number format"></s:textfield>`：Struts2 的标签，定义了一个手机号码框，它的 label 属性指定了手机号码框的标签名，name 属性指定了手机号码框的名称，tooltip 属性指定了手机号码框的提示信息。

18. `<s:textfield label="email" name="user.email" tooltip="input correct email format"></:textfield>`：Struts2 的标签，定义了一个邮箱框，它的 label 属性指定了邮箱框的标签名，name 属性指定了邮箱框的名称，tooltip 属性指定了邮箱框的提示信息。

19. `<s:submit label="Register"></:submit>`：Struts2 的标签，定义了一个提交按钮，它的 label 属性指定了按钮的标签名。

20. `</s:form>`：Struts2 的标签，结束表单的定义。

21. `</>`：HTML 页面的主体元素的结束标签。

22. `</html>`：HTML 页面的根元素的结束标。











9.
<%@ taglib uri="/struts-tags" prefix="s" %>

这是一个 JSP 页面的指令，用于导入 Struts2 的标签库。其中，uri 属性指定了标签库的路径，prefix 属性指定了标签库的前缀，使得可以使用 Struts2 的标签。在 JSP 页面中，使用 Struts2 的标签可以方地生成表单、链接、文本框等页面素，并且可以方便地与后台的 Java 代码进行交互。












10.
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Success Page</title>
</head>
<body>
    <h1>Your information:</h1> <br/>
    ${user}
</body>
</html>

这是一个 JSP 页面，用于显示用户注册成功后的信息。下面是对每一句代码的详细分析：

1. `<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>`：JSP 页面的指令，指定了页面的编码方式为 UTF-8。

2. `<!DOCTYPE html>`：HTML5 的文档类型声明。

3. `<html>`：HTML 页面的根元素。

4. `<head>`：HTML 页面的头部元素，用于定义页面的元数据。

5. `<meta http-equiv="Content-Type" content="text/html; charset-8">`：定义了页面的编码方式为 UTF-8。

6. `<title>Success Page</title>`：定义了页面的标题。

7. `</head>`：头部元素的结束标签。

8. `<body>`：HTML 页面的主体元素。

9. `<h1>Your information:</h1> <br/>：页面的标题，用于提示用户注册成功，并换行。

10. `${user}`：EL 表达式，用于显示用户的信息。在 Struts2 中，用户的信息会被封装在一个名为 user 的对象中，该对象可以通过 EL 表达式 ${user} 来访问。

. `</body>`：HTML 页面的主体元素的结束标签。

12. `</html>`：HTML 页面的根元素的结束标签。












11.
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         id="WebApp_ID" version="3.0">
  <display-name>FormValidate</display-name>
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

这是一个 web.xml 文件，用于配置 Web 应用程序的部署描述符。下面是对每一句代码的详细分析：

1. `<?xml version="10" encoding="UTF-8"?>`：XML 文件的声明，指定了 XML 的版本和编码方式。

2. `<web-app xmlns:xsi="httpwww.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd" id="WebApp_ID" version="3.0">`：Web 应用程序的根元素，其中包含了命名空间、模式位置、应用程序 ID 和号等信息。

3. `<display-name>FormValidate</display-name>`：Web 应用程序的显示名称，用于在 Web 服务器中显示。

4. `<filter>`：定义了一个过滤器，用于拦截请求并进行处理。

5. `<filter-name>struts2</filter-name>`：过滤器的名称，用于在其他地方引用该过滤器。

6. `<filter-class>.apache.struts2.dispatcher.filter.StrutsPrepareAndExecuteFilter</filter-class>`：过滤器的类名，用于指定过滤器的实现类。

7. `</filter>`：过滤器的结束标签。

8. `<filter-mapping>`：定义了一个过滤器映射，用于将过滤器与 URL 模式进行关联。

9. `<filter-name>struts2</filter-name>`：过滤器的名称，与上面定义的过滤器名称相同。

10. `<url-pattern>/*</url-pattern>`：URL 模式，用于指定过滤器要拦截的 URL。

11. `</-mapping>`：过滤器映射的结束标签。

12. `<welcome-file-list>`：定义了一个欢迎文件列表，用于指定 Web 应用程序的默认页面。

13. `<welcome-file>index.html</welcome-file>`：欢迎文件列表中的一个元素，指定了默认页面为 index.html。

14. `<welcome-file>index.htm</welcome-file>`：欢迎文件列表中的一个元素，指定了默认页面为 index.htm。

15. `<welcome-file>index.jsp</welcome-file>`：欢迎文件列表中的一个元素，指定了页面为 index.jsp。

16. `<welcome-file>default.html</welcome-file>`：欢迎文件列表中的一个元素，指定了默认页面为 default.html。

17. `<welcome-file>default.htm</welcome-file>`：欢迎文件列表中的一个元素指定了默认页面为 default.htm。

18. `<welcome-file>default.jsp</welcome-file>`：欢迎文件列表中的一个元素，指定了默认页面为 default.jsp。

19. `</welcome-file-list>`：欢迎文件列表的结束签。

20. `</web-app>`：Web 应用程序的结束标签。












12.
mvn jetty:run

`mvn jetty:run` 是 Maven 命令，用于启动 Jetty Web 服务器并运行当前 Maven 项目。这个命令会自动下载所需的依赖项并将它们打包成一个 WAR 文件，然后将 WAR 文件部署到 Jetty 服务器上并启动它。在运行这个命令之前，需要确保已经在项目的根目录下执行了 `mvn clean install` 命令，以确保项目已经被正确地编译和打包。





