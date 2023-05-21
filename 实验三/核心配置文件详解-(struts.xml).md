
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE struts PUBLIC
    "-//Apache Software Foundation//DTD Struts Configuration 2.5//EN"
    "http://struts.apache.org/dtds/struts-2.5.dtd">

<struts>

    <constant name="struts.enable.DynamicMethodInvocation" value="false" />
    <constant name="struts.devMode" value="true" />

    <package name="default" namespace="/" extends="struts-default">

        <default-action-ref name="index" />

        <global-results>
            <result name="error">/WEB-INF/jsp/error.jsp</result>
        </global-results>

        <global-exception-mappings>
            <exception-mapping exception="java.lang.Exception" result="error"/>
        </global-exception-mappings>

        <action name="index">
            <result type="redirectAction">
                <param name="actionName">HelloWorld</param>
                <param name="namespace">/example</param>
            </result>
        </action>
    </package>

    <include file="example.xml"/>

    <!-- Add packages here -->

</struts>

这是一个 Struts2 的配置文件，它使用 XML 格式编写。以下是每个元素的详细说明：

- `<?xml version="1.0" encoding="UTF-8" ?>`：这是 XML 文件的声明，它指定了 XML 版本和编码方式。
- `<!DOCTYPE struts PUBLIC "-//Apache Software Foundation//DTD Struts Configuration 2.5//EN" "http://struts.apache.org/dtds/struts-2.5.dtd">`：这是 Struts2 配置文件的文档类型声明，它指定了 Struts2 配置文件的 DTD 文件。
- `<struts>`：这是 Struts2 配置文件的根元素。
- `<constant>`：这是一个常量元素，它指定了一个 Struts2 常量。
- `name="struts.enable.DynamicMethodInvocation"`：这是一个常量名称属性，它指定了常的名称。
- `value="false"`：这是一个常量值属性，它指定了常量的值。
- `</constant>`：常量元素的结束标签。
- `<constant>`：这是一个常量元素，它指定了一个 Struts2 常量。
- `name="struts.devMode"`：这是一个常量名称属性，它指定了常量的名称。
- `value="true"`：这是一个常量值属性，它指定了常量的值。
- `</constant>`：常量元素的结束标签。
- `<package>`：这是一个包元素，它指定了一个 Struts2 包。
- `name="default"`：这是一个包名称属性，它指定了包的名称。
- `namespace="/" `：这是一个命名空间属性，它指定了包的命名空间。
- `extends="struts-default"`：这是一个继承属性，它指定了包继承的父包。
- `<default-action-ref>`：这是一个默认操作引用元素，它指定了默认操作。
- `name="index"`：这是一个操作名称属性，它指定了默认操作的名称。
- `</default-action-ref>`：默认操作引用元素的结束标签。
- `<global-results>`：这是一个全局结果元素，它指定了全局结果。
- `<result>`：这是一个结果元素，它指定了一个结果。
- `name="error"`：这是一个结果名称属性，它指定了结果的名称。
- `/WEB-INF/jsp/error.jsp`：这是一个结果值属性，它指定了结果的值。
- `</result>`：结果元素的结束标签。
- `</global-results>`：全局结果元素的结束标签。
- `<global-exception-mappings>`：这是一个全局异常映射元素，它指定了全局异常映射。
- `<exception-mapping>`：这是一个异常映射元素，它指定了一个异常映射。
- `exception="java.lang.Exception"`：这是一个异常名称属性，它指定了异常的名称。
- `result="error"`：这是一个结果属性，它指定了异常处理后的结果。
- `</exception-mapping>`：异常映射元素的结束标签。
- `</global-exception-mappings>`：全局异常映射元素的结束标签。
- `<action>`：这是一个操作元素，它指定了一个 Struts2 操作。
- `name="index"`这是一个操作名称属性，它指定了操作的名称。
- `<result>`：这是一个结果元素，它指定了操作的结果。
- `type="redirectAction"`：这是一个结果类型属性，它指定了结果的类型。
- `<param>`：这是一个参数元素，它指定了一个参数。
- `name="actionName"`：这是一个参数名称属性，它指定了参数的名称。
- `value="HelloWorld"`：这是一个参数值属性，它指定了参数的值。
- `</param>`：参数元素的结束标签。
 `<param>`：这是一个参数元素，它指定了一个参数。
- `name="namespace"`：这是一个参数名称属性，它指定了参数的名称。
- `value="/example"`：这是一个参数值属性，它指定了参数的值。
- `</param>`：参数元素的结束标签。
- `</result>`：结果元素的结束标签。
-</action>`：操作元素的结束标签。
- `</package>`：包元素的结束标签。
- `<include>`：这是一个包含元素，它用于包含其他配置文件。
- `file="example.xml"`：这是一个文件属性，它指定了要包含的文件。
- `</include>`：包含元素的结束标签。
- `</struts>`：Struts2 配置文件的结束标签。

总的来说，这个 Struts2 配置文件用于配置 Struts2 应用程序。它包含了常量、包、操作、结果等元素，用于指定 Struts2 应用程序的配置信息。









2.
<include file="**/**/***.xml" />

这是一个 XML 配置文件中的 `<include>` 元素，它用于包含其他的 XML 配置文件。其中 `file` 属性指定了要包含的文件的路径和名称，其中 `**` 表示任意目录，`*` 表示任意文件名。

例如，如果 `file` 属性的值为 `config/**/*.xml`，则表示要包含 `config` 目录下的所有子目录中的所有 XML 配置文件。

使用 `<include>` 元素可以将一个大的配置文件拆分成多个小的配置文件，使得配置更加清晰和易于维护。同时，也可以方便地重用已有的配置文件，提高发效率。







