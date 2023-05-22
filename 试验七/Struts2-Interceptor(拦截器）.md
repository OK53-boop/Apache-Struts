1.
InterceptorLogin
├── pom.xml
└── src
    └── main
        ├── java
        │   └── shiyanlou
        │       └── test
        │           ├── ApplyCode.java
        │           └── Login.java
        ├── resources
        │   └── structs.xml
        └── webapp
            ├── applyCode.jsp
            ├── index.jsp
            ├── success.jsp
            └── WEB-INF
                └── web.xml

这是一个基于 Struts2 的 Web 应用程序，其中包含一个名为 InterceptorLogin 的模块。让我解释一下其中的每一个部分：

1. `pom.xml`：Maven 项目的配置文件，用于管理项目依赖和构建配置。

2. `src/main/java/shiyanlou/test/`：Java 代码的根目录。

3. `ApplyCode.java`：一个 Java 类，用于处理申请代码的请求。

4. `Login.java`：一个 Java 类，用于处理用户登录的请求。

5. `src/main/resources/struts.xml`：Struts2 的配置文件，用于配置应用程序的为。

6. `webapp/`：Web 应用程序的根目录。

7. `applyCode.jsp`：一个 JSP 页面，用于显示申请代码的表单。

8. `index.jsp`：应用程序的主页。

9. `success.jsp`：一个 JSP 页面，用于显示申请代码成功的提示。

10. `WEB-INF/web.xml`：Web 应程序的部署描述符，用于配置应用程序的部署信息和 Servlet 容器的行为。










2.
public interface Interceptor extends Serializable {

    /**
     * Called to let an interceptor clean up any resources it has allocated.
     */
    void destroy();

    /**
     * Called after an interceptor is created, but before any requests are processed using
     * {@link #intercept(com.opensymphony.xwork2.ActionInvocation) intercept} , giving
     * the Interceptor a chance to initialize any needed resources.
     */
    void init();

    /**
     * Allows the Interceptor to do some processing on the request before and/or after the rest of the processing of the
     * request by the {@link ActionInvocation} or to short-circuit the processing and just return a String return code.
     *
     * @param invocation the action invocation
     * @return the return code, either returned from {@link ActionInvocation#invoke()}, or from the interceptor itself.
     * @throws Exception any system-level error, as defined in {@link com.opensymphony.xwork2.Action#execute()}.
     */
    String intercept(ActionInvocation invocation) throws Exception;

}

这是 Struts2 拦截器（Interceptor）接口的定义。让我解释一下其中的每一个部分：

1. `void destroy()`：在拦截器被销毁时调用，于清理拦截器所占用的资源。

2. `void init()`：在拦截器被创建后，但在任何请求被处理之前调，用于初始化拦截器所需的资源。

3. `String intercept(ActionInvocation invocation) throws Exception`：在请求被处理之前和/或之后，拦截器可以对请求进行一些处理，或者直接返回一个字符串返回码以终止请求的处理。该方法接收一个 ActionInvocation 对象，用于调用下一个拦截器 Action。该方法返回一个字符串返回码，可以是从 ActionInvocation 的 invoke() 方法返回的返回码，也可以是拦截器自己返回的返回码。如果在处理请求时发生系统级错误，则该方法将抛出一个 Exception 异常。











3.
public abstract class AbstractInterceptor implements Interceptor {

    /**
     * Does nothing
     */
    public void init() {
    }

    /**
     * Does nothing
     */
    public void destroy() {
    }

    /**
     * Override to handle interception
     */
    public abstract String intercept(ActionInvocation invocation) throws Exception;
}

这是 Struts2 拦截器（Interceptor）的抽象类，实现了 Interceptor 接口。让我解释一下其中的每一个部分：

1. `void init()`：实现了 Interceptor 接口中的 init() 方法但是该方法不做任何事情。

2. `void destroy()`：实现了 Interceptor 接口中的 destroy() 方法，但是该方法不做何事情。

3. `public abstract String intercept(ActionInvocation invocation) throws Exception`：实现了 Interceptor 接口中的 intercept() 方法，但是该方法是抽象的，需要子类实现。该方法接收一个 Action 对象，用于调用下一个拦截器 Action。该方法返回一个字符串返回码，可以是从 ActionInvocation 的 invoke() 方法返回的返回码，也可以是拦截器自己返回的返回码。如果在处理请求时发生系统级错误，则该方法将抛出一个 Exception 异。










4.
    @Override
    public String intercept(ActionInvocation invocation) throws Exception {
        ValueStack stack = invocation.getStack();
        CompoundRoot root = stack.getRoot();
        if (shouldCopyStack(invocation, root)) {
            copyStack(invocation, root);
        }
        return invocation.invoke();
    }
    
    
    这是 Struts2 拦截器（Interceptor）的一个示例方法，实现了 Interceptor 接口中的 intercept() 方法。让我解释一下其中的每一个部分：

1. `ValueStack stack = invocation.getStack()`：获取当前的 ValueStack 对象，用于访问请求中的数据。

2. `CompoundRoot root = stack.getRoot()`：获取 ValueStack 对象的根元素，用于访问请求中的数据。

3. `if (shouldCopyStack(invocation, root))`：判断是否需要复制 ValueStack 对象。这个方法是一个抽象方法，需要子实现。

4. `copyStack(invocation, root)`：复制 ValueStack 对象。这个方法是一个抽象方法，需要子类实现。

5. `return invocation.invoke()`：调用下一个拦截器或 Action，继续处理请求。如果方法返回一个字符串返回码，则请求处理将在此处终止。










5.
    /**
     * @throws ConfigurationException If no result can be found with the returned code
     */
    public String invoke() throws Exception {
        String profileKey = "invoke: ";
        try {
            UtilTimerStack.push(profileKey);

            if (executed) {
                throw new IllegalStateException("Action has already executed");
            }

            if (interceptors.hasNext()) {
                final InterceptorMapping interceptor = interceptors.next();
                String interceptorMsg = "interceptor: " + interceptor.getName();
                UtilTimerStack.push(interceptorMsg);
                try {
                                resultCode = interceptor.getInterceptor().intercept(DefaultActionInvocation.this);
                            }
                finally {
                    UtilTimerStack.pop(interceptorMsg);
                }
            } else {
                resultCode = invokeActionOnly();
            }

            // this is needed because the result will be executed, then control will return to the Interceptor, which will
            // return above and flow through again
            if (!executed) {
                if (preResultListeners != null) {
                    for (Object preResultListener : preResultListeners) {
                        PreResultListener listener = (PreResultListener) preResultListener;

                        String _profileKey = "preResultListener: ";
                        try {
                            UtilTimerStack.push(_profileKey);
                            listener.beforeResult(this, resultCode);
                        }
                        finally {
                            UtilTimerStack.pop(_profileKey);
                        }
                    }
                }

                // now execute the result, if we're supposed to
                if (proxy.getExecuteResult()) {
                    executeResult();
                }

                executed = true;
            }

            return resultCode;
        }
        finally {
            UtilTimerStack.pop(profileKey);
        }
    }
    
这是 Struts2 中的 DefaultActionInvocation 类的 invoke() 方法。让我解释一下其中的每一个部分：

1. `UtilTimerStack.push(profileKey)`：使用 UtilTimerStack 记录方法执行时间，profileKey 是一个字符串，用于标识当前方法。

2. `if (executed)`：检查 Action 是否已经执行过，如果已经执行过，则抛出 IllegalStateException 异常。

3. `if (interceptors.hasNext())`：检查是否还有拦截器需要执行。如果有，则获取下一个拦截器，并调用其 intercept 方法。

4. `resultCode = invokeActionOnly()`：如果没有拦截器需要执行，则调用 invokeActionOnly() 方法执行 Action。

5. `if (!executed)`：检查 Action 是否已经执行过。如果没有，则执行 preResultListeners 中的 PreResultListener 对象的 beforeResult() 方法。

6. `if (proxy.getExecuteResult())`：检查是否需要执行 Action 的结果。如果需要，则调用 executeResult() 方法执行结果。

7. `executed = true`：将 executed 标记为 true，表示 Action 已经执行过。

8. `return resultCode`：返回 Action 的结果代码。

9. `UtilTimerStack.pop(profileKey)`：使用 UtilTimerStack 记录方法执行时间，profileKey 是一个字符串，用于识当前方法。








6.
resultCode = interceptor.getInterceptor().intercept(DefaultActionInvocation.this);

这行代码是 Struts2 中的 DefaultActionInvocation 类的 invoke() 方法中的一部分。它调用了当前拦截器的 intercept() 方法，并将 DefaultActionInvocation 对象作为参数传递给该方法这个方法的返回值是一个字符串，表示拦截器执行后的结果代码。这个结果代码将被用于决定下一个拦截器或 Action执行流程。在这个代码行中，resultCode 变量被赋值为拦截器的执行结果。









7.
    @Override
    public String intercept(ActionInvocation invocation) throws Exception {
        ValueStack stack = invocation.getStack();
        CompoundRoot root = stack.getRoot();
        if (shouldCopyStack(invocation, root)) {
            copyStack(invocation, root);
        }
        return invocation.invoke();
    }
    
这是 Struts2 中的 Interceptor 接口的 intercept() 方法的一个实现。让我解释一下其中的每一个部分：

1. `ValueStack stack = invocation.getStack()`：获取 ActionInvocation 对象的 ValueStack 对象，用于访问 Action 的属性和方法。

2. `CompoundRoot root = stack.getRoot()`：获取 ValueStack 对象的根元素，即 CompoundRoot 对象。

3. `if (shouldCopyStack(invocation, root))`：检查是否需要复制 ValueStack 对象。如果需要，则调用 copyStack() 方法复制 ValueStack 对象。

4. `return invocation.invoke()`：调用 ActionInvocation 对象的 invoke() 方法，执行下一个拦截器或 Action。

在这个代码中，Interceptor 的主要作用是在 Action 执行或执行后对 ValueStack 对象进行处理。在这个实现中，Interceptor 检查是否需要复制 ValueStack 对象，并在需要时调用 copyStack() 方法进行复制。然后，Interceptor 调用 ActionInvocation 对象的 invoke 方法，执行下一个拦截器或 Action。最终，Interceptor 返回一个字符串，表示拦截器执行后的结果代码。










8.
public interface PreResultListener {

    /**
     * This callback method will be called after the {@link com.opensymphony.xwork2.Action} execution and
     * before the {@link com.opensymphony.xwork2.Result} execution.
     *
     * @param invocation  the action invocation
     * @param resultCode  the result code returned by the action (eg. <code>success</code>).
     */
    void beforeResult(ActionInvocation invocation, String resultCode);

}

这是 Struts2 中的 PreResultListener 接口。它定义了一个 beforeResult() 方法，该方法在 Action 执行后、Result 执行前被调用。该方法接收两个参数：ActionInvocation 对象和结果代码。在 beforeResult() 方法中，可以对 Action 的执行结果进行处理例如修改结果代码、添加一些额外的数据等等。这个接口的实现可以被注册到 Struts2 的配置文件中，以便在 Action 执行后对结果进行处理。










9.
@Override
public String intercept(ActionInvocation invocation) throws Exception {
    if (applyInterceptor(invocation)) {
        return doIntercept(invocation);
    }
    return invocation.invoke();
}

这是 Struts2 中的 Interceptor 接口的 intercept() 方法的一个实现。让我解释一下其中的每一个部分：

1. `if (applyInterceptor(invocation))`：检查是否需要应用拦截器。如果需要，则调用 doIntercept() 方法执行拦截器。

2. `return doIntercept(invocation)`：调用 doIntercept() 方法执行拦截器，并返回拦截器执行后的结果代码。

3. `return invocation.invoke()`：如果不需要应用拦截器，则调用 ActionInvocation 对象的 invoke() 方法，执行下拦截器或 Action。

在这个代码中，Interceptor 的主要作用是在 Action 执行或执行后对请求进行处理。在这个实现中，Interceptor 检查是否需要应用拦截器，并在需要时调用 doIntercept() 方法执行拦截器。然后， 返回一个字符串，表示拦截器执行后的结果代码。如果不需要应用拦截器，则调用 ActionInvocation 对象的 invoke() 方法，执行下一个拦截器或 Action。
    








10.
    /**
     * Subclasses must override to implement the interceptor logic.
     *
     * @param invocation the action invocation
     * @return the result of invocation
     * @throws Exception
     */
    protected abstract String doIntercept(ActionInvocation invocation) throws Exception;
    
    
    这是 Struts2 中的 Interceptor 抽象类的 doIntercept() 方法。该方法是一个抽象方法，需要在子类中进行实现。在 doIntercept() 方法中，可以对请求进行处理，例如修改请求参数、验证用户权限、记录日志等等。该方法接收一个 ActionInvocation 对象作为参数，并返回一个字符串，表示拦截器执行后的结果代码。在子类中实现 doIntercept() 方法时，需要根据具体的业务需求进行处理，并在必要时调用 ActionInvocation 对象的 invoke() 方法，执行下一个拦截器或 Action。
    
    
    
    
    
    
    
    
    
    
11.
wget http://labfile.oss.aliyuncs.com/courses/32/m2.zip
unzip m2.zip
mv .m2 /home/shiyanlou/

这是一组 Linux 命令，用于下载并解压一个名为 m2.zip 的文件，并将其中的 .m2 文件夹移动到 /home/shiyanlou/ 目录下。具体解释如下：

1. `wget http://labfile.oss.aliyuncs.com/courses/32/m2.zip`：使用 wget 命令下载一个名为 m2.zip 的文件，该文件位于 http://labfile.oss.aliyuncs.com/courses/32/ 的路径下。

2. `unzip m2.zip`：使用 unzip 命令解压 m2.zip 文件。

3. `mv .m2 /home/shiyanlou/`：使用 mv 命令将解压后的 .m2 文件夹移动到 /home/shiyanlou/ 目录下。注意，这里的 .m2 文件夹是以点开头的隐藏文件夹。









12.
mvn archetype:generate -DgroupId=shiyanlou -DartifactId=InterceptorLogin  -DarchetypeArtifactId=maven-archetype-webapp

这是一个 Maven 命令，用于创建一个名为 InterceptorLogin 的 Web 应用程序项目。具体解释如下：

1. `mvn archetype:generate`：使用 Maven 的 archetype 插件生成一个项目。

2. `-DgroupId=shiyanlou`：指定项目的 Group ID 为 shiyanlou。

3. `-DartifactId=InterceptorLogin`：指定项目的 Artifact ID 为 InterceptorLogin。

4. `-DarchetypeArtifactId=maven-archetype-webapp`：指定使用的 Maven Archetype 为 maven-archetype-webapp，即创建一个 Web 应用程序项目。

执行该命令后，Maven 将会在当前目录下创建一个名为 InterceptorLogin 的项目，并包含一个基本的 Web 应用程序结构。









13.
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>shiyanlou</groupId>
    <artifactId>InterceptorLogin</artifactId>
    <packaging>war</packaging>
    <version>1.0-SNAPSHOT</version>
    <name>InterceptorLogin Maven Webapp</name>
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
        <finalName>InterceptorLogin</finalName>
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

这是一个 Maven 的 POM 文件，用于配置 InterceptorLogin 项目的依赖和构建信息。具体解释如下：

1. `<project>`：定义 Maven 项目的根元素。

2. `xmlns="http://maven.apache.orgOM/4.0.0"`：指定 XML 命名空间。

3. `xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`：指定 XML Schema 实例命名空间。

4. `xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/m-v4_0_0.xsd"`：指定 XML Schema 的位置。

5. `<modelVersion>4.0.0</modelVersion>`：指定 POM 文件的版本。

6. `<groupId>shiyanlou</groupId>`：指定项目的 Group ID。

7.artifactId>InterceptorLogin</artifactId>`：指定项目的 Artifact ID。

8. `<packaging>war</packaging>`：指定项目的打包方式为 WAR。

9. `<version>1.0-SNAPSHOT</version>`：指定项目的版本号10. `<name>InterceptorLogin Maven Webapp</name>`：指定项目的名称。

11. `<dependencies>`：定义项目的依赖。

12. `<dependency>`：定义一个依赖。

13. `<groupId>org.struts</groupId>`：指定依赖的 Group ID。

14. `<artifactId>struts2-core</artifactId>`：指定依赖的 Artifact ID。

15. `<version>2.5.18</version>`：指定依赖的版本号。

16. `<dependency>`：定义另一个依赖。

17. `<groupId>javax.servlet</groupId>`：指定依赖的 Group ID。

18. `<artifactId>javax.servlet-api</artifactId>`：指定依赖的 Artifact ID。

19. `<version>4.0.1</version>`：指定依赖的版本号。

20. `<scope>provided</scope>`：指定依赖的作用范围为 provided，表示该依赖由容器提供。

21. `</dependencies>`：结束依赖的定义。

22. `<build>`定义项目的构建信息。

23. `<finalName>InterceptorLogin</finalName>`：指定项目构建后的名称。

24. `<plugins>`：定义项目的插件。

25. `<plugin>`：定义一个插件。

26. `<groupId>org.eclipse.jetty</groupId>`：指定插的 Group ID。

27. `<artifactId>jetty-maven-plugin</artifactId>`：指定插件的 Artifact ID。

28. `<version>9.4.12.v20180830</version>`：指定插件的版本号。

29. `<configuration>`：定义插件的信息。

30. `<scanIntervalSeconds>10</scanIntervalSeconds>`：指定插件扫描文件变化的时间间隔为 10 秒。

31. `<webApp>`：定义 Web 应用程序的配置信息。

32.contextPath>/</contextPath>`：指定 Web 应用程序的上下文路径为根路径。

33. `</webApp>`：结束 Web 应用程序的定义。

34. `</configuration>`：结束插件的配置信息。

35. `</plugin>`：结束插件的定义。

36. `</>`：结束插件的定义。

37. `</build>`：结束构建信息的定义。

38. `</project>`：结束 Maven 项目的定义。










14.
package shiyanlou.test.interceptor;

import java.util.Map;
import com.opensymphony.xwork2.ActionContext;

public class Login {

    // 登录成功后的消息 message
    private String msg;

    // 输入的邀请码
    private String inputCode;

    public String getMsg() {
        return msg;
    }

    public void setMsg(String msg) {
        this.msg = msg;
    }

    public String getInputCode() {
        return inputCode;
    }

    public void setInputCode(String inputCode) {
        this.inputCode = inputCode;
    }

    public String execute() throws Exception {

        // 从 session 中通过 “code” 这个 key 获取生成的邀请码
        Map map = ActionContext.getContext().getSession();
        String code = (String) map.get("code");

        // 注意 code 是 Session 中的，inputCode 是用户输入的
        if (code != null) {
            if ( null == getInputCode() || getInputCode().equals("") )  {
                // 向 Session 中提交，以便后面在页面中显示
                map.put("msgSession",  "Empty code!");
                return "login";
        }else if ( !getInputCode().equals(code) ) {
            map.put("msgSession",  "Invalid code!");
            return "login";
        }else {
            msg = "Congratulations! You've logged in!";
            return "success";
        }
    }

    msg = "Congratulations! You've logged in!";
    return "success";

    }
}

这是一个 Struts2 拦截器的示例代码，用于验证用户输入的邀请码是否正确。下面是每一句代码的详细分析：

1. `package shiyanlou.test.interceptor;`：声明该类所在的包。

2. `import java.util.Map;`：导入 java.util.Map 类。

3. `import com.opensymphony.xwork2.ActionContext;`：导入 com.opensymphony.xwork2.ActionContext 类。

4. `public class Login {`：定义一个名为 Login 的类。

5. `private String msg;`：声明一个名为 msg 的私有字符串类型变量。

6 `private String inputCode;`：声明一个名为 inputCode 的私有字符串类型变量。

7. `public String getMsg() {`：定义一个公有的返回字符串类型的 getMsg 方法。

8. `return msg;`：返回 msg 变量的值。

9. `public void setMsg(String msg) {`：定义一个公有的设置字符串类型的 setMsg 方法。

10. `this.msg = msg;`：将传入的参数值赋给 msg 变量。

11. `public String getInputCode() {`：定义一个公有的返回字符串类型的 getInputCode 方法。

12. `return inputCode;`：返回 inputCode 变量的值。

13. `public void setInputCode(String inputCode) {`：定义一个公有的设置字符串类型的 setInputCode 方法。

14. `this.inputCode = inputCode;`：将传入的参数值赋给 inputCode 变量。

15. `public String execute() throws Exception {`：定义一个公有的返回字符串类型的 execute 方法，可能会抛出异常。

16. `Map map = ActionContext.getContext().getSession();`：获取当前请求的 Session 对象。

17. `String code = (String) map.get("code");`：从 Session 中获取名为 "code" 的属性值，并将其转换为字符串类型。

18. `if (code != null) {`：如果 code 不为空。

19. `if ( null == getInputCode() || getInputCode().equals("") )  {`：如果 inputCode 为空或者为 ""。

20. `map.put("Session",  "Empty code!");`：向 Session 中添加名为 "msgSession" 的属性，并将其值设置为 "Empty code!"。

21. `return "login";`：返回字符串 "login"。

22. `}else if ( !getInputCode().equals(code) ) {`：如果 inputCode 不为空且不等于 code。

23. `map.put("msgSession",  "Invalid code!");`：向 Session 中添加名为 "msgSession" 的属性，并将其值设置为 "Invalid code!"。

24. `return "login";`：返回字符串 "login"。

25. `}else {`：如果 inputCode 不为空且等于 code。

26. `msg = "Congratulations! You've logged in!";`：将 msg 变量的值设置 "Congratulations! You've logged in!"。

27. `return "success";`：返回字符串 "success"。

28. `}`：结束 if 语句块。

29. `msg = "Congratulations! You've logged in!";`：将 msg 变量的值设置为 "Congratulations! You've logged in!"。

30. `return "success";`：返回字符串 "success"。

31. `}`：结束 execute 方法。

以上就是该 Struts2 拦截器示例代码的详细分析。









15.
package shiyanlou.test.interceptor;

import java.util.Map;
import com.opensymphony.xwork2.Action;
import com.opensymphony.xwork2.ActionInvocation;
import com.opensymphony.xwork2.interceptor.Interceptor;

public class ApplyCode  implements Interceptor {

    /**
     *
     */
    private static final long serialVersionUID = 1L;

    public void destroy() {
        // TODO Auto-generated method stub

    }

    public void init() {
        // TODO Auto-generated method stub

    }

    public String intercept(ActionInvocation arg0) throws Exception {
        // TODO Auto-generated method stub

        // 同样是从 session 中获得邀请码
        Map sessionMap = arg0.getInvocationContext().getSession();
        String code = (String) sessionMap.get("code");

        // 如果 session 中已经加入了这个邀请码，则交给 invoke() 函数处理
        if ( null != code && code.equals("shiyanlou") ) {
            return arg0.invoke();
        }

        // 否则就提示先申请一个邀请码 注入到 Session 中，以便在页面中显示
        sessionMap.put("msgSession",  "Apply a code first!");
        return "login";
    }
}

这段代码是一个 Struts2 拦截器，用于检查用户是否已经输入了正确的邀请码。下面是对每一句代码的详细分析：

1.package shiyanlou.test.interceptor;`：声明了该类所在的包。

2. `import java.util.Map;`：导入了 `java.util.Map` 类，用于存储 session 中的数据。

3. `import com.opensymphony.xwork2.Action;`：导入了 `com.opensymphony.xwork2.Action` 类，用于定义 Struts2 的 Action。

4. `import com.opensymphony.xwork2.ActionInvocation`：导入了 `com.opensymphony.xwork2.ActionInvocation` 类，用于定义 Struts2 的 ActionInvocation。

5. `import com.opensymphony.xwork2.interceptor.Interceptor;`：导入了 `com.opensymphony.xwork2.interceptor.Interceptor` 类，用于定义 Struts2 的拦截器。

6. `public class ApplyCode  implements Interceptor {`：定义了一个名为 `ApplyCode` 的类，实现了 `Interceptor` 接口，表示这是一个 Struts2 的拦截器。

7. `private static final long serialVersionUID = 1L;`：定义了一个静态的 long 类型的变量 `serialVersionUID`，用序列化和反序列化对象。

8. `public void destroy() {`：实现了 `Interceptor` 接口中的 `destroy()` 方法，用于销毁拦截器。

9. `public void init() {`：实现了 `Interceptor` 接口中的 `init()` 方法，用于初始化拦截器。

10. `public String intercept(ActionInvocation arg0) throws Exception {`：实现了 `Interceptor` 接口中的 `intercept()` 方法，用于拦截请求并进行处理。

11. `Map sessionMap = arg0.getInvocationContext().getSession();`：获取当前请求的 session 对象，并将其存储在 `sessionMap` 变量中。

12. `String code = (String) sessionMap.get("code");`：从 session 中获取名为 `code` 的属性，并将其转换为字符串，存储在 `code` 变量中。

13. `if ( null != code && code.equals("shiyanlou") ) {`：如果 `code` 不为空且等于 "shiyanlou"，执行下面的代码块。

14. `return arg0.invoke();`：调用 `ActionInvocation` 对象的 `invoke()` 方法，继续执行后续的拦截器或 Action。

15. `sessionMap.put("msgSession",  "Apply a code first!");`：将名为 `msgSession` 的存储在 session 中，属性值为 "Apply a code first!"。

16. `return "login";`：返回名为 "login" 的字符串，表示跳转到登录页面。











16.
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="s" uri="/struts-tags" %>
<!DOCTYPE html>
<html>
<head>
<title>Login Interceptor</title>
</head>
<body>

   <center><h2>${sessionScope.msgSession }</h2>
    <s:form action="login" method="post">
        <s:textfield label="INVITATION CODE" name="inputCode"></s:textfield>
        <s:submit value="Login" />
    </s:form>

    <a href="/applyCode.jsp" type="button" >Apply a code</a>

    </center>

</body>
</html>

这段代码是一个 JSP 页面，用于显示登录界面和提示信息。下面是对每一句代码的详细分析：

1. `<%@ page language="java" contentType="text/html charset=UTF-8" pageEncoding="UTF-8"%>`：指定页面的编码格式为 UTF-8。

2 `<%@ taglib prefix="s" uristruts-tags" %>`：导入 Struts2 的标签库，以便在页面中使用 Struts2 的标签。

3. `<!DOCTYPE html>`：声明文档类型为 HTML。

4. `<html>`：开始 HTML 标签5. `<head>`：开始 head 标签，用于定义文档的头部信息。

6 `<title>Login Interceptor</title>`：定义页面的标题为 "Login Interceptor"。

7. `</head>`：结束 head 标签。

8. `<body>`：开始 body 标签，用于定义文档的主体内容。

9. `<center>`：开始 标签，用于将页面中的内容居中显示。

10. `<h2>${sessionScope.msgSession }</h2>`：显示名为 `msgSession` 的 session 属性的值。

11. `<s:form action="" method="post">`：使用 Struts2 的表单标签，定义一个名为 "login" 的 Action。

12. `<s:textfield label="INVITATION CODE" name="inputCode"></s:textfield>`：使用 Struts2 的文本框标签，定义一个名为 "inputCode" 的文本框，并设置标签为 "INVITATION CODE"。

13. `<s:submit value="Login" />`：使用 Struts2 的提交按钮标签，定义一个名为 "Login" 的提交按钮。

14. `</s:form>`：结束 Struts2 的表单标签。

15. `<a href="/applyCode.jsp" type="button" >Apply a code</a>`：定义一个超链接，指向名为 "applyCode.jsp" 的页面，用于申请邀请码。

16. `</center>`：结束 center 标签。

17. `</body>`结束 body 标签。

18. `</html>`：结束 HTML 标签。









17.
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Apply a new code</title>
</head>
<body>
<%
  request.getSession().setAttribute("code", "shiyanlou");
  %>
your INVITATION CODE is :  <b>shiyanlou</b> <br/>
<a href="/index.jsp" type="button" >Back to login</a>
</body>
</html>
    
这段代码是一个 JSP 页面，用于生成新的邀请码并显示在页面上。下面是对每一句代码的详细分析：

1. `<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="-8"%>`：指定页面的编码格式为 UTF-8。

2. `<!DOCTYPE html>`：声明文档类型为 HTML。

3. `<html>`：开始 HTML 标签。

4. `<head>`：开始 head 标签，用于定义文档的头部信息。

5. `<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">`：指定页面的编码格式为 UTF-8。

6. `<title>Apply a new code</title>`：定义页面的标题为 "Apply a new code"。

7. `</head>`：结束 head 标签。

8. `<body：开始 body 标签，用于定义文档的主体内容。

9. `<%`：开始 Java 代码块。

10. `request.getSession().setAttribute("code", "shiyanlou");`：在 session 中设置名为 "code" 的属性，属性值为 "shiyanlou"。

11. `%>`：结束 Java 代码块。

12. `your INVITATION CODE is :  <b>shiyanlou</b> <br/>`：显示新生成的邀请码。

13. `<a href="/index.jsp" type="button" > to login</a>`：定义一个超链接，指向名为 "index.jsp" 的页面，用于返回登录页面。

14. `</body>`：结束 body 标签。

15. `</html>`：结束 HTML 标签。
    
    
    
    
    




18.
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="s" uri="/struts-tags" %>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Hello World</title>
</head>
<body>
     <s:property value="msg"/>
</body>
</html>
    
这段代码是一个 JSP 页面，用于显示一个 Struts2 Action 中的属性值。下面是对每一句代码的详细分析：

1. `< page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>`：指定页面的编码格式为 UTF-8。

2 `<%@ taglib prefix="s" uri="/struts-tags" %>`：导入 Struts2 的标签库，以便在页面中使用 Struts2 的标签。

3. `<!DOCTYPE html>`：声明文档类型为 HTML。

4. `<html>`：开始 标签。

5. `<head>`：开始 head 标签，用于定义文档的头部信息。

6. `<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">`：指定页面的编码格式为 UTF-8。

7. `<title>Hello World</title>`：定义页面的标题为 "Hello World"。

8. `</head>`：结束 head 标签。

9. `<body>`：开始 body 标签，用于定义文档的主体内容。

10. `<s:property value="msg"/>`：使用 Struts2 的属性标签，显示名为 "msg" 的 Action 属性的值。

11. `</body>`：结束 body 标签。

12. `</html>`：结束 HTML 标签。
    
    
    
    
    
    
    
    
    
    
19.
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE struts PUBLIC
    "-//Apache Software Foundation//DTD Struts Configuration 2.5//EN"
    "http://struts.apache.org/dtds/struts-2.5.dtd">
<struts>
    <package name="shiyanlou.interceptor" extends="struts-default">
        <interceptors>
            <interceptor name="applyCode" class="shiyanlou.test.interceptor.ApplyCode"></interceptor>
            <interceptor-stack name="interceptLogin">
                <interceptor-ref name="applyCode"></interceptor-ref>
                <interceptor-ref name="defaultStack"></interceptor-ref>
            </interceptor-stack>
        </interceptors>
        <default-action-ref name="index" />
        <action name="index" >
            <result name="success">/index.jsp</result>
        </action>
        <action name="login" class="shiyanlou.test.interceptor.Login" method="execute">
            <result name="success">/success.jsp</result>
            <result name="login">/index.jsp</result>
            <interceptor-ref name="interceptLogin"></interceptor-ref>
        </action>
    </package>
</struts>
    
这段代码是一个 Struts2 的配置文件，用于配置拦截器和 Action。下面是对每一句代码的详细分析：

1. `<?xml version="1.0"="UTF-8" ?>`：声明 XML 版本和编码格式。

2. `<!DOCTYPE struts PUBLIC "-//Apache Foundation//DTD Struts Configuration 2.5//EN" "http://struts.apache.org/dtds/struts-2.5.dtd">`：声明 Struts2 配置文件的 DTD。

3. `<struts>`：开始 Struts2 配置文件。

4. `< name="shiyanlou.interceptor" extends="struts-default">`：定义一个名为 "shiyanlou.interceptor" 的包，继承自 Struts2 默认包。

5. `<interceptors>`：开始拦截器配置。

6. `<interceptor name="applyCode" class="shiyanlou.test.interceptor.ApplyCode"></interceptor>`：定义一个名为 "applyCode" 的拦截器，使用 "shiyanlou.test.interceptor.ApplyCode" 类实现7. `<interceptor-stack name="interceptLogin">`：定义一个名为 "interceptLogin" 的拦截器栈。

8. `<interceptor-ref name="applyCode"></interceptor-ref>`：将 "applyCode" 拦截器添加到拦截器栈中。

9. `<interceptor-ref name="defaultStack"></interceptor-ref>`：将 Struts2 默认拦截器栈添加到拦截器栈中。

10. `</interceptor-stack>`：结束拦截器栈配置。

11. `</interceptors>`：结束拦截器配置。

12. `<default-action-ref name="index" />`：定义默认的 Action，如果请求的 Action 不存在，则使用名为 "index" 的 Action。

13. `<action name="index" >`：定义一个名为 "index" 的 Action。

14. `<result name="success">/index.jsp</result>`：定义 Action 执行成功后的返回结果，跳转到名为 "index.jsp" 的页面。

15. `</action>`：结束 Action 配置。

16. `<action name="login" class="shiyanlou.test.interceptor.Login" method="execute">`：定义一个名为 "login" 的 Action，使用 "shiyanlou.test.interceptor.Login" 类实现，执行 "execute" 方法。

17. `<result name="success">/success.jsp</result>`：定义 Action 执行成功后的返回结果，跳转到名为 "success.jsp" 的页面。

18. `<result name="login">/index.jsp</result>`：定义 Action 执行失败后的返回结果，跳转到名为 "index.jsp" 的页面。

19. `<interceptor-ref name="interceptLogin"></interceptor-ref>`：将 "interceptLogin" 拦截器栈添加到 Action 中。

20. `</action>`：结束 Action 配置。

21. `</package>`：结束包配置。

22. `</struts>`：结束 Struts2 配置文件。
    
    
    
    
    
    
    
    
    
    
20.
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         id="WebApp_ID" version="3.0">
  <display-name>InterceptorLogin</display-name>
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
    
这是一个 Java Web 应用程序的 web.xml 配置文件，用于配置应用程序的过滤器和欢迎页面。下面是对每一句代码的详细分析：

1. `<?xml version="1.0" encoding="UTF-8"?>`：声明 XML 版本和编码格式。

2. `<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd" id="WebApp_ID" version="3.0">`：开始 Web 应用程序配置，指定 XML 命名空间和版本。

3. `<display-name>InterceptorLogin</display-name>`：定义应用程序的显示名称。

. `<filter>`：开始过滤器配置。

5. `<filter-name>struts2</filter-name>`：定义过滤器的名称。

6. `<filter-class>org.apache.struts2.dispatcher.filter.StrutsPrepareAndExecuteFilter</filter-class>`：定义过滤器的类名，用于处理 Struts2 请求。

7. `</filter>`：结束过滤器配置。

8. `<filter-mapping>`：开始过滤器映射配置。

9. `<filter-name>struts2</filter-name>`：指定要映射的过滤器名称。

10. `<url-pattern>/*</url-pattern>`：指定要映射的 URL 模式，这里是所有 URL。

11. `</filter-mapping>`：结束过滤器映射配置。

12. `<welcome-file-list>`：开始欢迎页面配置。

13. `<welcome-file>index.html</welcome-file>`：定义一个欢迎页面，如果存在，则显示名为 "index.html" 的页面。

14. `<welcome-file>index.htm</welcome-file>`：定义一个欢迎页面，如果存在，则显示名为 "index.htm" 的页面。

15. `<welcome-file>index.jsp</welcome-file>`：定义一个欢迎页面，如果存在，则显示名为 "index.jsp" 的页面。

16. `<welcome-file>default.html</welcome-file>`：定义一个欢迎页面，如果存在，则显示名为 "default.html" 的页面。

17. `<welcome-file>default.htm</welcome-file>`：定义一个欢迎页面，如果存在，则显示名为 "default.htm" 的页面。

18. `<welcome-file>default.jsp</welcome-file>`：定义一个欢迎页面，如果存在，则显示名为 "default.jsp" 的页面。

19. `</welcome-file-list>`：结束欢迎页面配置。

20. `</web-app>`：结束 Web 应用程序配置。
    
    
    
    
    

