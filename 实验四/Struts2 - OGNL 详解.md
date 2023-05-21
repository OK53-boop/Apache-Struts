1.
<body>
    Hello World, Welcome! <s:property value="name"/>
</body>

这是一个简单的 Struts2 JSP 页面，其中包含一个 `<body>` 元素和一个 `<s:property>` 标签。`<s:property>` 标签用于显示一个名为 `name` 的属性的值。

当这个 JSP 页面被渲染时，`<s:property>` 标签将被 Struts2 框架解析，并将 `name` 属性的值插入到页面中。如果 `name` 属性的值为 "John"，则页面将显示 "Hello World, Welcome! John"。

这个 JSP 页面可以作为 Struts2 应用程序的一个视图，用于显示动态生成的内容。通过使用 Struts2 标签库，可以轻松地将数据从控制器传递到视图，并在页面中显示。









2.
<s:set name="mySet" value="#{'key1':'value1','key2':'value2'}" />
<s:property value="#mySet['key1']"/>   //输出的是 value1
<s:url value="#mySet['key1']" />      //输出的是#mySet['key1']
<s:url value="%{#mySet['key1']}"/>   //输出的是 value1

这是一个 Struts2 JSP 页面，其中包含了 `<s:set>`、`<s:property>` 和 `<s:url>` 标签。`<s:set>` 标签用于创建一个名为 `mySet` 的变量，并将一个包含两个键值对的 Map 对象赋值给它。`<s:property>` 标签用于输出 `mySet` 变量中 `key1` 对应的值 `value1`。`<s:url>` 标签用于生成一个 URL，其中 `value` 属性的值为 `#mySet['key1']`，但是由于 `#` 符号是特殊字符，所以它会被转义成字符串 "#mySet['key1']"。最后 `<s:url>` 标签使用了 OGNL 表达式 `%{#mySet['key1']}`，它会被 Struts2 框架解析成 `value1`，因此输出的是 `value1`。

这个例子展示了 Struts2 框架中使用 OGNL 表达式的能力。OGNL 是一种强大的表达式语言，可以用于访问和操作 Java 对象的属性和方法。在 Struts2 中，OGNL 表达式可以用于访问和操作 Action 类中的属性和方法，以及在 JSP 页面中访问和操作变量和对象。









3.
<field-validator type="stringlength">
            <param name="maxLength">18</param>
               <param name="minLength">6</param>
               <param name="trim">true</param>
            <message>密码强度必须在 ${minLength}到${maxLength} 之间！</message>
        </field-validator>

这是一个 Struts2 验证器配置，它使用了 `stringlength` 类型的验证器。该验证器用于验证一个字符串的长度是否在指定的范围内，并可以选择是否去除字符串的前导和尾随空格。在这个例子中，`maxLength` 参数被设置为 18，`minLength` 参数被设置为 6，`trim` 参数被设置为 true，表示在验证之前需要去除字符串的前导和尾随空格。

如果验证失败，将会显示一条错误消息，其中包含了 `${minLength}` 和 `${maxLength}` 变量的值。这些变量将被 Struts2 框架解析，并替换为相应的参数值。例如，如果 `minLength` 参数的值为 6，`maxLength` 参数的值为 18，那么错误消息将显示为 "密码强度必须在 6 到 18 之间！"。

这个例子展示了 Struts2 框架中验证器的使用。验证器可以用于验证表单数据的有效性，并在验证失败时显示错误消息。Struts2 框架提供了许多内置的验证器类型，也可以自定义验证器来满足特定的需求。











4.
<!-- 1. 访问 Value Stack 中 action 的普通属性 -->
<s:property value="name"/>

<!-- 2. 访问 Value Stack 中对象的普通属性（要有 get set 方法） -->
<!-- 第一种方式 -->
<s:property value="user.age"/>

<!-- 第二种方式 -->
<s:property value="user['age']"/>

<!-- 错误方法 -->
<!-- <s:property value="user[age]"/> -->

<!-- 3. 调用 Value Stack 中对象的普通方法 -->
<s:property value="user.setName('master')" /> | 结果显示：<s:property value="user.name"/> //输出结果为 “结果显示：master”

<!-- 4. 调用 Value Stack 中 action 属性的方法 -->
<s:property value="name.length()"/>

<!-- 5. 调用 Value Stack 中 action 的普通方法 -->
<s:property value="add()" />

<!-- 6. 调用普通类的构造方法 -->
<s:property value="new user.User()"/> //实例化一个对象

这是一个 Struts2 JSP 页面，其中包含了多个 `<s:property>` 标签，用于访问和操作 Value Stack 中的属性和方法。Value Stack 是 Struts2 框架的一个重要概念，它是一个栈结构，用于存储 Action 类和 JSP 页面中的变量和对象。在 JSP 页面中，使用 `<s:property>` 标签来访问和操作 Value Stack 中的属性和方法。

在这个例子中，第一个 `<s:property>` 标签用于访问 Value Stack 中 Action 类的 `name` 属性。第二个和第三个 `<:property>` 标签用于访问 Value Stack 中对象 `user` 的 `age` 属性，其中第二个标签使用了点号语法，第三个标签使用了方括号语法。需要注意的是，方括号语法中的属性名必须用引号括起来。

第四个 `<s:>` 标签用于调用 Value Stack 中对象 `user` 的 `setName` 方法，并将其参数设置为字符串 "master"。第五个 `<s:property 标签用于调用 Value Stack 中 Action 类的 `add` 方法。第六个 `<s:property>` 标签用于实例化一个 `user.User` 类的对象。

这个例子展示了 Struts2 框架中访问和操作 Value Stack 的能力。Value Stack 是 Struts2 框架中非常重要的一个概念，它可以用于在 Action 类和 JSP 页面中传递数据，并且支持访问和操作属性和方法。








5.
/* 访问静态属性表达式的格式为：@[类全名（包括包路径）]@[值名] */
<s:property value="@action.UserAction@index"/>

这是一个 Struts2 JSP 页面，其中包含了一个 `<s:property>` 标签，用于访问静态属性。在 Struts2 框架中，访问静态属性需要使用特定的语法格式，即 `@[类全名]@[值名]`。其中，类全名包括包路径，值名为静态属性的名称。

在这个例子中，`@actionAction@index` 表示访问 `action` 包下的 `UserAction` 类的 `index` 静态属性。`<s:property>` 标签将会输出该静态属性的值。

需要注意的是，访问静态属性需要使用 `@` 符号作为前缀，并且类全名和值名之间需要使用 `@` 符号进行分隔。这个语法格式只适用于访问静态属性，如果要访问普通属性或方法，需要使用其他的语法格式。










6.
/* 调用静态方法表达式的格式为：@[类全名（包括包路径）]@[方法名] */
<s:property value="@action.UserAction@getInstance()"/>

这是一个 Struts2 JSP 页面，其中包含了一个 `<s:property>` 标签，用于调用静态方法。在 Struts2 框架中，调用静态方法需要使用特定的语法格式，即 `@[类全名]@[方法名]()`。，类全名包括包路径，方法名为静态方法的名称，后面需要跟上一对空括号。

在这个例子中，`action.UserAction@getInstance()` 表示调用 `action` 包下的 `UserAction` 类的 `getInstance` 静态方法。`<s:property>` 标签将会输出该静态方法的返回值。

需要注意的是，调用静态方法需要使用 `@` 符号作为前缀，并且类全名和方法名之间需要使用 `@` 符号进行分隔。方法名后面需要跟上一对空括号。这个语法格式只适用于调用静态方法，如果要调用普通方法，需要使用其他的语法格式。









7.
<s:property value="@@max(2, 3)" />

这是一个 Struts2 JSP 页面，其中包含了一个 `<s:property>` 标签，用于调用静态方法。在 Struts2 框架中，调用静态方法需要使用特定的语法格式，即 `@[类全名]@[方法名]()`。类全名包括包路径，方法名为静态方法的名称，后面需要跟上一对空括号。

在这个例子中，`@@max(2, 3)` 表示调用 Java 中的 `Math` 类的 `max` 静态方法，并传入参数 2 和 3。需要注意的是，由于 `@` 符号是用于表示静态方法调用的前缀，因此在调用 `Math` 类的静态方法时，需要在面加上一个额外的 `@` 符号，以避免与静态方法调用的语法格式冲突。

`<s:property>` 标签将输出该静态方法的返回值，即 3。

需要注意的是，调用静态方法需要使用 `@` 符号作为前缀，并且类全名和方法名之间需要使用 `@` 符号进行分隔。方法名后面需要跟上一对空号。这个语法格式只适用于调用静态方法，如果要调用普通方法，需要使用其他的语法格式。










8.
<s:property value="userlist"/>

这是一个 Struts2 JSP 页面，其中包含了一个 `<s:property>` 标签，用于输出一个名为 `userlist` 的变量的值。在uts2 框架中，可以通过在 Action 类中定义一个名为 `userlist` 的属性，并提供相应的 getter 方法，来将该属性的值传递给 JSP 页面。

在这个例子中，`<s:property>` 标签将会输出 `userlist` 变量的值。具体的值取决于在 Action 类中如何设置该变量的值。如果该变量是一个 List 类型的对象，那么 `<s:property>` 标签将会输出该 List 中的所有元素。

需要的是，`<s:property>` 标签用于输出变量的值，而不是变量名本身。如果要输出变量名本身，可以 `<s:text>` 标签。例如，`<s:text name="userlist" />` 将会输出字符串 "userlist"。









9.
<s:property value="userlist[1]"/>

这是一个 Struts2 JSP 页面，其中包含了一个 `<s:property>` 标签，用于输出一个名为 `userlist` 的 List 变量中的第二个元素。在 Struts2 框架中，可以通过在 类中定义一个名为 `userlist` 的 List 属性，并提供相应的 getter 方法，来将该属性的值传递给 JSP 页面。

在这例子中，`<s:property>` 标签将会输出 `userlist` 变量中的第二个元素。需要注意的是，List 中的元素是从 0 开始编号的，因此 `userlist[1]` 表示 List 中的第二个元素。

需要的是，`<s:property>` 标签用于输出变量的值，而不是变量名本身。如果要输出变量名本身，可以使用 `<s:text>` 标签。例如，`<s:text name="userlist" />` 将会输出字符串 "userlist"。









10.
<s:property value="userlist.{age}"/>

这是一个 Struts2 JSP 页面，其中包含了一个 `<s:property>` 标签，用于输出一个名为 `userlist` 的 List 变量中所有元素的 `age` 属性。在 Struts2 框架中，可以通过在类中定义一个为 `userlist` 的 List 属性，并提供相应的 getter 方法，来将该属性的值传递给 JSP 页面。

在这个例子中，<s:property>` 标签将会输出 `userlist` 变量中所有元素的 `age` 属性。需要注意的是，这里使用了 Struts2 的 OGNL 表达式语法，其中 `{age}` 表示获取对象的 `age` 属性。这个语法格式可以用于获取对象的属性值，或者调用对象的方法。

需要的是，`<s:property>` 标签用于输出变量的值，而不是变量名本身。如果要输出变量名本身，可以使用 `<s:text>` 标签。例如，`<s:text name="user" />` 将会输出字符串 "userlist"。










11.
<!-- 第一种方法 ( 不常用 ) -->
<s:property value="userlist.{age}[0]"/>

<!-- 第二种方法 -->
<s:property value="userlist[0].age"/>

这是一个 Struts2 JSP 页面，其中包含了两种方法用于输出一个名为 `userlist` 的 List 变量中第一个元素的 `age` 属性。在 Struts2 框架中，可以通过在类中定义一个为 `list` 的 List 属性，并提供相应的 getter 方法，来将该属性的值传递给 JSP 页面。

第一种方法使用了 Struts2 的 OGNL 表达式语法，其中 `{age}` 表示获取对象的 `age` 属性，`[0]` 表示获取 List 中的第一个元素。这种方法不太常用，因为它需要在 OGNL 表达式中使用两个操作符。

第二种方法更加简单，直接使用了 List 中第一个元素的 `age` 属性。这种方法更加直观，也更容易理解。

需要的是，`<s:property>` 标签用于输出变量的值，而不是变量名本身。如果要输出变量名本身，可以使用 `<s:text>` 标签。例如，`<s:text="userlist" />` 将会输出字符串 "userlist"。









12.
<s:property value="userSet"/>

这是一个 Struts2 JSP 页面，其中包含了一个 `<s:property>` 标签，用于输出一个名为 `userSet` 的 Set 变量。在 Struts2 框架，可以通过在类中定义一个名为 `userSet` 的 Set 属性，并提供相应的 getter 方法，来将该属性的值传递给 JSP 页面。

在这个例子中，`<s:property>` 标签将会输出 `userSet` 变量中所有元素的字符串表示形式。需要注意的是，Set 中的元素是无序的，因此输出的顺序可能会不同。

需要的是，`<s:property>` 标签用于输出变量的值，而不是变量名本身。如果要输出变量名本身，可以使用 `<s:text>` 标签。例如，`<s:text name="userSet" />` 将会输出字符串 "userSet"。










13.
<!-- 错误方法 -->
<s:property value="userSet[0]"/>

这是一个 Struts2 JSP 页面，其中包含了一个 `<s:property>` 标签，用于输出一个名为 `userSet` 的 Set 变量中第一个元素。在 Struts2 框架，通过在类中定义一个名为 `userSet` 的 Set 属性，并提供相应的 getter 方法，来将该属性的值传递给 JSP 页面。

注意的是，Set 中的元素是无序的，因此不能通过索引来获取 Set 中的元素。因此，`<s:property value="userSet[0]"/>` 这种方法是错误的，会导致运行时错误。

如果需要获取 Set 中的元素，可以使用迭代器或者 foreach 循环来遍历 Set 中的元素。例如：

```
<s:iterator value="userSet">
    <s:property />
</s:iterator>
```

这个例子中，`<s:iterator>` 标签用于遍历 `userSet` 变量中的所有元素，`<s:property>` 标签用于输出每个元素的表示形式。










14.
<s:property value="userMap"/>

这是一个 Struts2 JSP 页面，其中包含了一个 `<s:property>` 标签，用于输出一个名为 `userMap` 的 Map 变量。在 Struts2 框架，可以通过在类中一个名为 `userMap` 的 Map 属性，并提供相应的 getter 方法，来将该属性的值传递给 JSP 页面。

在这个例子，`<s:property>` 标签将会输出 `userMap` 变量中所有键值对的字符串表示形式。需要注意的是，Map 中的键值对是无序的，因此输出的顺序可能会不同。

需要的是，`<s:property>` 标签用于输出变量值，而不是变量名本身。如果要输出变量名本身，可以使用 `<s:text>` 标签。例如，`<s:text name="userMap" />` 将会输出字符串 "userMap"。










15.
<!-- 第一种方式 -->
<s:property value="userMap.user1"/>

<!-- 第二种方式 -->
<s:property value="userMap['user1']"/> |  <s:property value="userMap[\"user1\"]"/>

这些代码片段是使用Struts2框架编写的，用于显示用户映射中的某个值。以下是对这两种方式的解释：

第一种方式：
<s:property value="userMap.user1"/>
这种方式使用点号(.)来访问userMap中的"user1"键对应的值。

第二种方式：
<s:property value="userMap['user1']"/> 或 <s:property value="userMap[\"user1\"]"/>
这种方式使用方括号([])来访问userMap中的"user1"键对应的值。这里有两种表示方法，一种是使用单引号(')，另一种是使用转义的双引号(\")。

这两种方式都可以实现相同的功能，即从userMap中获取"user1"键对应的值并显示出来。在实际应用中，可以根据具体需求和编码习惯选择合适的方式。










16.
<s:property value="userMap.keys"/>

这是一个Java代码片段，它使用了Java中的Map数据结构，并调用了Map的keys()方法来获取Map中所有键的集合。具体来说，这段代码返回了一个包含Map中所有键的Set集合。










17.
<s:property value="userMap.values"/>

这是一个Java代码片段，它使用了Java中的Map数据结构，并调用了Map的values()方法来获取Map中所有值的集合。具体来说，这段代码返回了一个包含Map中所有值的集合。









18.
<s:property value="userMap.size()"/> | <s:property value="userMap.size"/>

这是一个Java代码片段，它使用了Java中的Map数据结构，并调用了Map的size()方法来获取Map中键值对的数量。具体来说，这段代码返回了Map中键值对的数量。

这段代码有两种写法，一种是使用括号将方法参数括起来，另一种是直接使用方法名。这两种写法都可以正确地调用Map的size()方法，返回Map中键值对的数量。









19.
<!-- OGNL 过滤集合的语法为：collection.{?expression} -->
<s:property value="userlist.{?#this.age>1}"/>  //获取到的是 age>1 的对象集合

这是一个Struts2中使用OGNL表达式的代码片段，它使用了OGNL语法中的过滤集合的语法，即.{?expression}，来过滤userlist集合中符合条件的对象。

具体来说，这段代码使用了#this关键字来表示当前对象，然后通过#this.age>1的表达来判断当前对象的age属性是否大于1，如果是，则将该对象加入到返回的集合中。因此，这段代码返回的是user集合中所有age大于1的对象集合。









20.
<s:property value="userlist.{^#this.age>1}.{age}"/>  //获取到满足 age>1 集合的第一个对象的 age

<s:property value="userlist.{$#this.age>1}.{age}"/>  //获取到满足 age>1 集合的最后一个对象的 age

这是一个Struts2中使用OGNL表达式的代码片段，它使用了OGNL语法中的过滤集合的语法，即.{?expression}，来过滤userlist集合中合条件的对象，并获取满足条件的对象的age属性。

具体来说，第一个代码片段使用了^操作符来获取满足#this.age>1条件的集合中的第一个对象，然后使用.age来获取该对象的age属性。因此，这段代码返回的是userlist集合中满足age>1条件的第一个对象的age属性。

第二个代码片段使用了$操作符来获取满足#this.age>1条件的集合中的最后一个对象，然后使用.age来获取该对象的age属性。因此，这段代码返回是userlist集合中满足age>1条件的最后一个对象的age属性。









21.

