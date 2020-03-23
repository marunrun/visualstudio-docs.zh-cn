---
title: 调试技术和工具
description: 通过使用 Visual Studio 修复异常、修复错误和改进代码，编写更好的代码，减少错误
ms.custom:
- debug-experiment
- seodec18
ms.date: 02/14/2020
ms.topic: conceptual
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2ac595098d793e44d65312a09fc8857225f150ef
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301019"
---
# <a name="debugging-techniques-and-tools-to-help-you-write-better-code"></a>调试技术和工具，帮助您编写更好的代码

修复代码中的 Bug 和错误可能是一项耗时（有时甚至是令人沮丧的）任务。 学习如何有效地调试需要时间，但像 Visual Studio 这样的强大 IDE 可以使您的工作轻松得多。 IDE 可以帮助您修复错误并更快地调试代码，而不仅仅是这样，它还可以帮助您用更少的 Bug 编写更好的代码。 本文的目的是让您全面了解"错误修复"过程，以便您知道何时使用代码分析器、何时使用调试器、如何修复异常以及如何编写意图代码。 如果您已经知道需要使用调试器，请参阅[首先查看调试器](../debugger/debugger-feature-tour.md)。

在本文中，我们将讨论利用 IDE 提高编码会话的效率。 我们涉及几个任务，例如：

* 利用 IDE 的代码分析器准备用于调试的代码

* 如何修复异常（运行时错误）

* 如何通过编码意图（使用断言）来最小化 Bug

* 何时使用调试器

为了演示这些任务，我们展示了一些在尝试调试应用时会遇到的最常见的错误和错误类型。 尽管示例代码为 C#，但概念信息通常适用于 Visual Studio 支持C++、视觉基本语言、JavaScript 和其他语言（除非另有说明）。 屏幕截图为 C#。

## <a name="create-a-sample-app-with-some-bugs-and-errors-in-it"></a>创建包含一些错误和错误的示例应用

以下代码有一些可以使用 Visual Studio IDE 修复的错误。 此处的应用程序是一个简单的应用程序，用于模拟从某些操作获取 JSON 数据、将数据反序列化到对象以及使用新数据更新简单列表。

创建应用：

1. 您必须安装 Visual Studio 并安装 **.NET Core 跨平台开发**或 **.NET 桌面开发**工作负载，具体取决于要创建的应用类型。

    如果您尚未安装 Visual Studio，请转到 Visual [Studio 下载](https://visualstudio.microsoft.com/downloads/) 页面以免费安装它。

    如果您需要安装工作负载，但已有可视化工作室，请单击 **"工具** > **获取工具和功能**"。 Visual Studio 安装程序启动。 选择 **.NET 核心跨平台开发**或 **.NET 桌面开发**工作负载，然后选择 **"修改**"。

1. 打开 Visual Studio。

    ::: moniker range=">=vs-2019"
    在“开始”窗口上，选择“创建新项目”****。 在搜索框中键入**控制台**，然后选择**控制台应用 （.NET 核心）** 或**控制台应用程序 （.NET 框架）**。 选择“下一步”。**** 键入项目名称，如**Console_Parse_JSON，** 然后单击"**创建**"。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中，选择 **"文件** > **新项目** > **"。** 在 **"新建项目**"对话框的左侧窗格中，在**Visual C#** 下，选择**控制台应用**，然后在中间窗格中选择**控制台应用 （.NET Core）** 或**控制台应用 （.NET Framework）。** 键入**Console_Parse_JSON等**名称，然后单击 **"确定**"。
    ::: moniker-end

    如果您没有看到**控制台应用 （.NET Core）** 或**控制台应用 （.NET Framework）** 项目模板，请**Tools** > 转到**工具获取工具和功能**，这将打开可视化工作室安装程序。 选择 **.NET Core 跨平台开发**或 **.NET 桌面开发**工作负载，然后选择 **"修改**"。

    Visual Studio 创建控制台项目，该项目显示在右窗格的“解决方案资源管理器”中。

1. 将项目*Program.cs*文件中的默认代码替换为下面的示例代码。

```csharp
using System;
using System.Collections.Generic;
using System.Runtime.Serialization.Json;
using System.Runtime.Serialization;
using System.IO;

namespace Console_Parse_JSON
{
    class Program
    {
        static void Main(string[] args)
        {
            var localDB = LoadRecords();
            string data = GetJsonData();

            User[] users = ReadToObject(data);

            UpdateRecords(localDB, users);

            for (int i = 0; i < users.Length; i++)
            {
                List<User> result = localDB.FindAll(delegate (User u) {
                    return u.lastname == users[i].lastname;
                    });
                foreach (var item in result)
                {
                    Console.WriteLine($"Matching Record, got name={item.firstname}, lastname={item.lastname}, age={item.totalpoints}");
                }
            }

            Console.ReadKey();
        }

        // Deserialize a JSON stream to a User object.
        public static User[] ReadToObject(string json)
        {
            User deserializedUser = new User();
            User[] users = { };
            MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(json));
            DataContractJsonSerializer ser = new DataContractJsonSerializer(users.GetType());

            users = ser.ReadObject(ms) as User[];

            ms.Close();
            return users;
        }

        // Simulated operation that returns JSON data.
        public static string GetJsonData()
        {
            string str = "[{ \"points\":4o,\"firstname\":\"Fred\",\"lastname\":\"Smith\"},{\"lastName\":\"Jackson\"}]";
            return str;
        }

        public static List<User> LoadRecords()
        {
            var db = new List<User> { };
            User user1 = new User();
            user1.firstname = "Joe";
            user1.lastname = "Smith";
            user1.totalpoints = 41;

            db.Add(user1);

            User user2 = new User();
            user2.firstname = "Pete";
            user2.lastname = "Peterson";
            user2.totalpoints = 30;

            db.Add(user2);

            return db;
        }
        public static void UpdateRecords(List<User> db, User[] users)
        {
            bool existingUser = false;

            for (int i = 0; i < users.Length; i++)
            {
                foreach (var item in db)
                {
                    if (item.lastname == users[i].lastname && item.firstname == users[i].firstname)
                    {
                        existingUser = true;
                        item.totalpoints += users[i].points;

                    }
                }
                if (existingUser == false)
                {
                    User user = new User();
                    user.firstname = users[i].firstname;
                    user.lastname = users[i].lastname;
                    user.totalpoints = users[i].points;

                    db.Add(user);
                }
            }
        }
    }

    [DataContract]
    internal class User
    {
        [DataMember]
        internal string firstname;

        [DataMember]
        internal string lastname;

        [DataMember]
        // internal double points;
        internal string points;

        [DataMember]
        internal int totalpoints;
    }
}
```

## <a name="find-the-red-and-green-squiggles"></a>找到红色和绿色的波浪！

在尝试启动示例应用并运行调试器之前，请检查代码编辑器中的代码有红色和绿色波浪。 这些表示 IDE 的代码分析器标识的错误和警告。 红色波浪是编译时间错误，必须先修复这些错误，然后才能运行代码。 绿色波浪是警告。 尽管您通常可以在不修复警告的情况下运行应用，但它们可能是 Bug 的来源，并且通常通过调查它们来节省自己的时间和麻烦。 如果您喜欢列表视图，这些警告和错误也会显示在 **"错误列表"** 窗口中。

在示例应用中，您将看到需要修复的几个红色波浪，以及一个要查看的绿色波浪。 这是第一个错误。

![显示为红色波浪形的错误](../debugger/media/write-better-code-red-squiggle.png)

要修复此错误，您将查看 IDE 的另一个功能，该功能由灯泡图标表示。

## <a name="check-the-light-bulb"></a>检查灯泡！

第一个红色波浪表示编译时的错误。 将鼠标悬停在它上，然后```The name `Encoding` does not exist in the current context```您看到消息。

请注意，此错误在左下角显示一个灯泡图标。 与![螺丝刀图标螺丝刀图标](../ide/media/screwdriver-icon.png)一起，灯泡图标![灯泡图标](../ide/media/light-bulb-icon.png)表示快速操作，可帮助您修复或重构代码内联。 灯泡表示*应*修复的问题。 螺丝刀适用于您可能选择修复的问题。 使用第一个建议的修复程序通过单击左侧的 **"系统.文本**"来解决此错误。

![使用灯泡修复代码](../debugger/media/write-better-code-missing-include.png)

单击此项目时，Visual Studio 会在`using System.Text`*Program.cs*文件的顶部添加语句，红色波浪形将消失。 （如果您不确定建议的修复程序将执行什么操作，请先在应用修复程序之前选择右侧的 **"预览更改"** 链接。

前面的错误通常是通过向代码添加新`using`语句来解决的。 有几个常见的类似错误，例如```The type or namespace `Name` cannot be found.```这些类型的错误可能指示缺少程序集引用（右键单击项目，选择**添加** > **引用**），拼写错误的名称，或缺少需要添加的库（对于 C#，右键单击项目并选择 **"管理 NuGet 包**"）。

## <a name="fix-the-remaining-errors-and-warnings"></a>修复剩余的错误和警告

在此代码中还有一些波浪形。 在这里，您将看到一个常见的类型转换错误。 将鼠标悬停在波浪上时，您会看到代码正在尝试将字符串转换为 int，除非您添加显式代码进行转换，否则不支持 int。

![类型转换错误](../debugger/media/write-better-code-conversion-error.png)

由于代码分析器无法猜测您的意图，因此这次没有灯泡可以帮助您。 要修复此错误，您需要了解代码的意图。 在此示例中，不难看出该`points`值应该是一个数字（整数）值，因为您正在尝试添加到`points``totalpoints`中。

要修复此错误，从中`points`更改`User`类的成员：

```csharp
[DataMember]
internal string points;
```

更改为：

```csharp
[DataMember]
internal int points;
```

代码编辑器中的红色波浪线消失。

接下来，将鼠标悬停在`points`数据成员声明中的绿色波浪形上。 代码分析器告诉您该变量永远不会分配值。

![未分配变量的警告消息](../debugger/media/write-better-code-warning-message.png)

通常，这表示需要修复的问题。 但是，在示例应用中，您实际上是在反序列化过程中将数据`points`存储在变量中，然后将该值添加到`totalpoints`数据成员中。 在此示例中，您知道代码的意图，并可以安全地忽略警告。 但是，如果要消除该警告，可以替换以下代码：

```csharp
item.totalpoints = users[i].points;
```

替换为以下内容：

```csharp
item.points = users[i].points;
item.totalpoints += users[i].points;
```

绿色的波浪消失了。

## <a name="fix-an-exception"></a>修复异常

修复了所有红色波浪，并解决了所有绿色波浪，或者至少被调查，就可以启动调试器并运行应用了。

按**F5** （**调试>开始调试**）或"调试工具栏中![开始调试"开始调试](../debugger/media/dbg-tour-start-debugging.png "“调试”")。 **Start Debugging**

此时，示例应用将引发异常`SerializationException`（运行时错误）。 也就是说，应用程序会阻塞它尝试序列化的数据。 由于您在调试模式下启动应用（已连接调试器），调试器的异常帮助程序将直接带您到引发异常的代码，并为您提供有用的错误消息。

![发生序列化异常](../debugger/media/write-better-code-serialization-exception.png)

错误消息指示不能将值`4o`解析为整数。 因此，在此示例中，您知道数据是坏的：`4o`应该是`40`。 但是，如果您在实际方案中无法控制数据（假设您是从 Web 服务获取数据），您该怎么办？ 如何解决此问题？

当您遭遇异常时，您需要提出（并回答）几个问题：

* 此异常是否只是您可以修复的 Bug？ 或者，

* 此异常是您的用户可能会遇到的？

如果是前者，修复错误。 （在示例应用中，这意味着修复错误数据。如果是后者，您可能需要使用块处理代码中的异常（我们将在下一`try/catch`节中查看其他可能的策略）。 在示例应用中，替换以下代码：

```csharp
users = ser.ReadObject(ms) as User[];
```

替换为此代码：

```csharp
try
{
    users = ser.ReadObject(ms) as User[];
}
catch (SerializationException)
{
    Console.WriteLine("Give user some info or instructions, if necessary");
    // Take appropriate action for your app
}
```

块`try/catch`具有一些性能成本，因此您只想在真正需要它们时使用它们，即 （a） 它们可能发生在应用的发布版本中，以及 （b） 方法的文档指示您应该检查异常（假设文档已完成！ 在许多情况下，您可以适当地处理异常，用户将永远不会知道它。

以下是异常处理的几个重要提示：

* 避免使用空 catch 块（`catch (Exception) {}`如 ）不采取适当的操作来暴露或处理错误。 空或非信息化 catch 块可以隐藏异常，并使代码更难调试，而不是更容易。

* 在示例`try/catch`应用中，使用引发异常的特定函数周围的块（`ReadObject`。 如果在较大的代码块周围使用它，则最终会隐藏错误的位置。 例如，不要在调用父函数`try/catch``ReadToObject`（此处显示）周围使用块，否则您无法确切知道异常发生的位置。

    ```csharp
    // Don't do this
    try
    {
        User[] users = ReadToObject(data);
    }
    catch (SerializationException)
    {
    }
    ```

* 对于应用中包含的不熟悉的函数，尤其是与外部数据（如 Web 请求）交互的函数，请查看文档以查看该函数可能会引发哪些异常。 这对于正确处理错误和调试应用来说可能是关键信息。

对于示例应用`SerializationException`，通过更改为`GetJsonData``4o``40`修复 方法中的 。

## <a name="clarify-your-code-intent-by-using-assert"></a>使用断言阐明代码意图

单击调试工具栏 **（Ctrl** + **Shift** + **F5**） 中的**Restart**![重新启动应用](../debugger/media/dbg-tour-restart.png "重启应用")按钮。 这将以更少的步骤重新启动应用。 您可以在控制台窗口中看到以下输出。

![输出中的空值](../debugger/media/write-better-code-using-assert-null-output.png)

您可以在此输出中看到不太正确的内容。 **第**三条记录的名称和**姓氏**为空！

这是一个讨论有用的编码实践的好时机，这种练习通常使用不足，即在函数中使用`assert`语句。 通过添加以下代码，可以包含运行时检查，以确保 和`firstname``lastname`不是`null`。 替换`UpdateRecords`方法中的以下代码：

```csharp
if (existingUser == false)
{
    User user = new User();
    user.firstname = users[i].firstname;
    user.lastname = users[i].lastname;
```

替换为以下内容：

```csharp
// Also, add a using statement for System.Diagnostics at the start of the file.
Debug.Assert(users[i].firstname != null);
Debug.Assert(users[i].lastname != null);
if (existingUser == false)
{
    User user = new User();
    user.firstname = users[i].firstname;
    user.lastname = users[i].lastname;
```

通过在开发`assert`过程中向函数添加类似这样的语句，可以帮助指定代码的意图。 在前面的示例中，我们指定以下内容：

* 名字需要有效的字符串
* 姓氏需要有效的字符串

通过以这种方式指定意图，可以强制实施您的要求。 这是一种简单而方便的方法，可用于在开发过程中显示 Bug。 （`assert`语句也用作单元测试中的主要元素。

单击调试工具栏 **（Ctrl** + **Shift** + **F5**） 中的**Restart**![重新启动应用](../debugger/media/dbg-tour-restart.png "重启应用")按钮。

> [!NOTE]
> 代码`assert`仅在调试生成中处于活动状态。

重新启动时，调试器将`assert`暂停语句，因为表达式`users[i].firstname != null`将计算到`false`而不是`true`。

![断言解析为 false](../debugger/media/write-better-code-using-assert.png)

该`assert`错误告诉您存在需要调查的问题。 `assert`可以涵盖许多不一定看到异常的情况。 在此示例中，用户不会看到异常，并且`null`将添加值，如`firstname`记录列表中所示。 这可能会导致以后出现问题（如您在控制台输出中看到的），并且可能更难调试。

> [!NOTE]
> 在调用`null`值上的方法的方案中，将生成`NullReferenceException`结果。 通常希望避免对常规异常（`try/catch`即未绑定到特定库函数的异常）使用块。 任何对象都可以引发`NullReferenceException`。 如果不确定，请查看库功能的文档。

在调试过程中，最好保留特定`assert`语句，直到您知道需要将其替换为实际的代码修复程序。 假设您决定用户在应用的发布版本中可能会遇到异常。 在这种情况下，必须重构代码，以确保你的应用不会引发致命异常或导致一些其他错误。 因此，要修复此代码，请替换以下代码：

```csharp
if (existingUser == false)
{
    User user = new User();
```

替换为此代码：

```csharp
if (existingUser == false && users[i].firstname != null && users[i].lastname != null)
{
    User user = new User();
```

通过使用此代码，您可以满足代码要求，并确保未将 具有`firstname`或`lastname``null`值的记录添加到数据中。

在此示例中，我们在循环中添加了两`assert`个语句。 通常，在使用`assert`时，最好在函数或`assert`方法的入口点（开头）添加语句。 您当前正在查看示例应用中`UpdateRecords`的方法。 在此方法中，您知道如果任一方法参数是`null`，则请用函数入口点处的语句`assert`检查它们。

```csharp
public static void UpdateRecords(List<User> db, User[] users)
{
    Debug.Assert(db != null);
    Debug.Assert(users != null);
```

对于前面的语句，您的意图是加载现有数据 （`db`） 并在更新任何内容之前`users`检索新数据 （ ）。

可以将解析为`assert``true`或`false`的任何类型的表达式一起使用。 因此，例如，您可以添加这样的`assert`语句。

```csharp
Debug.Assert(users[0].points > 0);
```

如果要指定以下意图，则上述代码很有用：更新用户记录需要大于零 （0） 的新点值。

## <a name="inspect-your-code-in-the-debugger"></a>在调试器中检查代码

好了，现在你已经修复了示例应用出错的所有关键内容，您可以转到其他重要内容！

我们向您展示了调试器的异常帮助程序，但调试器是一个更强大的工具，它还允许您执行其他操作，如步进代码并检查其变量。 这些更强大的功能在许多方案中非常有用，尤其是：

* 您正在尝试在代码中隔离运行时 Bug，但无法使用前面讨论的方法和工具执行此操作。

* 您希望验证代码，即在代码运行时监视它，以确保代码按预期方式运行，并执行您期望的方式。

    在代码运行时监视代码是很有启发性的。 您可以通过这种方式了解有关代码的更多详细信息，并且通常可以在 Bug 出现任何明显症状之前识别它们。

要了解如何使用调试器的基本功能，请参阅[绝对初学者的调试](../debugger/debugging-absolute-beginners.md)。

## <a name="fix-performance-issues"></a>修复性能问题

另一种错误包括低效代码，这些代码会导致应用运行缓慢或使用过多的内存。 通常，优化性能是您在应用开发后期完成的事情。 但是，您可以尽早遇到性能问题（例如，您看到应用的某些部分运行缓慢），并且可能需要尽早使用分析工具测试应用。 有关分析工具（如 CPU 使用工具和内存分析器）的详细信息，请参阅[首先查看分析工具](../profiling/profiling-feature-tour.md)。

## <a name="next-steps"></a>后续步骤

在本文中，您已经了解如何避免和修复代码中的许多常见错误以及何时使用调试器。 接下来，详细了解如何使用 Visual Studio 调试器修复 Bug。

> [!div class="nextstepaction"]
> [零基础调试](../debugger/debugging-absolute-beginners.md)
