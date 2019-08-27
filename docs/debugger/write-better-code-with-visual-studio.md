---
title: 调试技术和工具
description: 使用 Visual Studio 以修复异常、 修复错误，并改进您的代码编写更好的代码更少 bug
ms.custom:
- debug-experiment
- seodec18
ms.date: 01/24/2019
ms.topic: conceptual
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8b34e23b1bc7972563d6d8d014ba0728dc637b34
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66262136"
---
# <a name="debugging-techniques-and-tools-to-help-you-write-better-code"></a>调试技术和工具可帮助你编写更好的代码

在代码中修复的 bug 和错误可能非常耗时-和有时令人沮丧-任务。 它需要时间来了解如何有效地调试，但功能强大的 IDE，类似于 Visual Studio 可以使您的工作变得更加轻松。 IDE 可帮助您修复错误并更快地调试代码并不只是的但它还可以帮助您编写更好的代码更少的 bug。 我们在本文中的目标是为您提供全面了解"错误修复"的进程，因此您将知道何时使用代码分析工具，何时使用调试器，如何修复异常，以及如何编写代码的意图。 如果您已经知道需要使用调试器，请参阅[先来看一下调试器](../debugger/debugger-feature-tour.md)。

在本文中，我们介绍如何利用 IDE 进行编码会话提高工作效率。 我们提到了多项任务，例如：

* 准备您的代码进行调试通过利用 IDE 的代码分析器

* 如何修复异常 （运行时错误）

* 如何最大程度减少编写代码的意图 （使用 assert） 的 bug

* 何时使用调试器

为了演示这些任务，我们介绍几种最常见的错误和调试您的应用程序时，将会遇到的 bug 类型。 尽管此示例代码C#，概念的信息是通常适用于C++，Visual Basic、 JavaScript 和 Visual Studio （除非另有说明） 支持其他语言。 屏幕截图为 C#。

## <a name="create-a-sample-app-with-some-bugs-and-errors-in-it"></a>某些 bug 和错误在其中创建示例应用

下面的代码完全可以使用 Visual Studio IDE 来修复一些 bug。 应用此处是一个简单的应用，用于模拟从某项操作，反序列化到对象，数据和使用新数据更新的简单列表获取的 JSON 数据。

创建应用：

1. 打开 Visual Studio，然后选择**文件** > **新建** > **项目**。 下**可视化C#** ，选择**Windows Desktop**或 **.NET Core**，然后在中间窗格中选择**控制台应用**。

    > [!NOTE]
    > 如果没有看到“控制台应用程序”项目模板，请单击“新建项目”对话框左侧窗格中的“打开 Visual Studio 安装程序”链接    。 Visual Studio 安装程序启动。 选择“.NET Core 桌面开发”或“.NET Core 跨平台开发”工作负载，然后选择“修改”    。

2. 在中**名称**字段中，键入**Console_Parse_JSON**然后单击**确定**。 Visual Studio 随即创建项目。

3. 在项目中的默认代码替换*Program.cs*具有下面的示例代码文件。

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

## <a name="find-the-red-and-green-squiggles"></a>查找红色和绿色波形曲线 ！

在尝试启动示例应用程序并运行调试器之前，检查在代码编辑器中的红色和绿色波形曲线的代码。 这些表示错误和警告的标识由 IDE 的代码分析器。 红色波浪线是编译时错误，这必须在之前修复可以运行代码。 绿色波浪线都是警告。 尽管您通常可以运行您的应用程序而修复这些警告，但它们可以是 bug 的源和您通常可省去时间和麻烦通过调查这些。 这些警告和错误也会出现在**错误列表**窗口中，如果您愿意列表视图。

在示例应用中，可以看到多个红色的波浪线，您需要修复，而您将看到在一个绿色的另一个在。 下面是第一个错误。

![显示为红色的波浪线时出错](../debugger/media/write-better-code-red-squiggle.png)

若要修复此错误，您将看到在 IDE 中，通过灯泡图标表示的另一项功能。

## <a name="check-the-light-bulb"></a>检查有灯泡图标中 ！

第一个红色的波浪线表示编译时错误。 悬停在其上方，看到消息```The name `Encoding` does not exist in the current context```。

请注意，此错误会显示到左下角的灯泡图标。 以及螺丝刀图标![螺丝刀图标](../ide/media/screwdriver-icon.png)，灯泡图标![灯泡图标](../ide/media/light-bulb-icon.png)表示快速操作可帮助你修复或重构代码内联。 灯泡图标表示问题*应*修复。 可以选择要修复的问题是螺丝刀。 使用第一个建议的修复方法来解决此错误，通过单击**使用 System.Text**左侧。

![使用灯泡修复代码](../debugger/media/write-better-code-missing-include.png)

单击此项，在 Visual Studio 添加`using System.Text`顶部的语句*Program.cs*文件和红色波浪线将消失。 (当不能确定建议的修复方法将执行哪些操作时，选择**预览更改**应用修补程序之前在右侧的链接。)

之前的错误是一个通常添加一个新的解决问题的常见`using`到你的代码语句。 如有几个常见的、 类似错误与此```The type or namespace `Name` cannot be found.```这些类型的错误可能表示缺少的程序集引用 (右键单击该项目中，选择**添加** > **引用**)，一个拼写错误的名称或需要将添加一个缺少库 (为C#，右键单击项目，然后选择**管理 NuGet 包**)。

## <a name="fix-the-remaining-errors-and-warnings"></a>修复的剩余错误和警告

有几个更多的波形曲线，若要查看在此代码中。 这里，您会看到常见的类型转换错误。 当悬停在波形曲线上时，可以看到该代码尝试将字符串转换为 int，除非添加显式代码以使转换不受支持。

![类型转换错误](../debugger/media/write-better-code-conversion-error.png)

由于代码分析器无法猜出你的意图，没有灯泡有助于出这一次。 若要修复此错误，您需要知道代码的目的。 在此示例中，它不太难看出`points`应该是一个数值 （整数） 的值，因为你尝试添加`points`到`totalpoints`。

若要解决此错误，请更改`points`的成员`User`从此类：

```csharp
[DataMember]
internal string points;
```

更改为：

```csharp
[DataMember]
internal int points;
```

在代码编辑器中红色的波浪线消失。

接下来，将鼠标悬停绿色波浪线中的声明`points`数据成员。 代码分析器会告诉您该变量永远不会分配一个值。

![未赋值的变量的警告消息](../debugger/media/write-better-code-warning-message.png)

通常情况下，这表示需要修复的问题。 但是，在示例应用中实际存储中的数据`points`变量在反序列化过程中，并将该值与`totalpoints`数据成员。 在此示例中，可以知道代码的目的和可以放心地忽略该警告。 但是，如果你想要消除该警告，您可以将以下代码：

```csharp
item.totalpoints = users[i].points;
```

替换为以下内容：

```csharp
item.points = users[i].points;
item.totalpoints += users[i].points;
```

绿色波浪线将消失。

## <a name="fix-an-exception"></a>修复异常

当你已经修复所有红色波形曲线和解析-或至少调查-所有绿色波形曲线，已准备好启动调试器并运行应用。

按 F5（“调试”>“开始调试”）或调试工具栏中的“开始调试”按钮（![开始调试](../debugger/media/dbg-tour-start-debugging.png "Start Debugging")）    。

在此情况下，示例应用程序将引发`SerializationException`异常 （运行时错误）。 也就是说，应用程序采用浅压深正在尝试进行序列化的数据。 在调试模式下 （附加调试器） 启动应用，因为调试器的异常帮助器将转到引发异常，并提供有用的错误消息的代码权限。

![SerializationException 发生](../debugger/media/write-better-code-serialization-exception.png)

错误消息指示您的值`4o`无法分析为整数。 因此，在此示例中，您知道数据无效：`4o`应为`40`。 但是，如果你不是真实的情况下 （例如从 web 服务获取） 中的数据控件中，您会怎么做一下？ 如何解决此问题？

遇到一个异常，需要提出 （和回答） 几个问题：

* 是此异常仅可修复的 bug？ 或者，

* 此异常是您的用户可能会遇到的某些内容？

如果是前者，修复 bug。 （在示例应用中，这意味着修复错误数据。）如果是后者，你可能需要处理的异常在代码中`try/catch`块 （我们介绍下一节中的其他可能的策略）。 在示例应用中，将以下代码：

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

一个`try/catch`块都有一定的性能开销，因此将只想要使用它们在真正需要时，即，其中 (a) 它们可能会出现应用程序的发行版本中，并且 (b) 文档方法指示你应检查的异常 （假设文档已完成 ！）。 在许多情况下，可以适当地处理异常和用户将永远不需要了解它。

下面是几个异常处理的重要提示：

* 避免使用空的 catch 块中，例如`catch (Exception) {}`，不采用适当的措施来公开或处理错误。 为空或非信息性的 catch 块可以隐藏异常，并且可以使代码更难以调试而不是变得更容易。

* 使用`try/catch`引发的异常的特定函数的块 (`ReadObject`，示例应用程序中)。 如果你使用它周围的代码的较大区块，则最终会隐藏错误的位置。 例如，不要使用`try/catch`围绕对父函数调用的块`ReadToObject`，此处显示，或者您不会知道该异常发生的确切位置。

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

* 对于不熟悉函数包含在应用中，尤其是那些与外部数据 （例如 web 请求） 进行交互，检查文档以查看该函数是可能会引发哪些异常。 这可能是正确的错误处理和调试您的应用程序的关键信息。

有关示例应用中，修复`SerializationException`中`GetJsonData`方法通过更改`4o`到`40`。

## <a name="clarify-your-code-intent-by-using-assert"></a>通过使用断言，明确你代码的意图

单击调试工具栏中的“重启”![重启应用](../debugger/media/dbg-tour-restart.png "RestartApp")按钮 (Ctrl + Shift + F5)     。 这更少的步骤中重新启动该应用程序。 请参阅控制台窗口中的以下输出。

![在输出中的 null 值](../debugger/media/write-better-code-using-assert-null-output.png)

您可以看到此不完全正确的输出中的某些内容。 **名称**并**lastname**的第三个记录都保留为空 ！

这是的好时机谈一谈有所帮助编码实践，往往未充分使用，就是使用`assert`函数中的语句。 通过添加以下代码，包括运行时检查，确保`firstname`并`lastname`不是`null`。 中的以下代码替换为`UpdateRecords`方法：

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

通过添加`assert`像这样的陈述到函数在开发过程中，可帮助指定代码的意图。 在前面的示例中，我们指定以下项：

* 有效的字符串是所必需的第一个名称
* 有效的字符串是所必需的最后一个名称

通过以这种方式指定意图，您强制执行你的要求。 这是简单方便的方法，您可以使用图面上的 bug 在开发过程。 (`assert`语句也可用作单元测试中的主要元素。)

单击调试工具栏中的“重启”![重启应用](../debugger/media/dbg-tour-restart.png "RestartApp")按钮 (Ctrl + Shift + F5)     。

> [!NOTE]
> `assert`代码处于活动状态仅在调试版本中。

重新启动时，调试器会暂停上`assert`语句，因为表达式`users[i].firstname != null`的计算结果为`false`而不是`true`。

![断言解析为 false](../debugger/media/write-better-code-using-assert.png)

`assert`错误告知你是否有需要调查的问题。 `assert` 可以包含很多情况下将不一定出现异常。 在此示例中，用户不会看到异常，和一个`null`值获取将添加为`firstname`列表中的记录。 这可能会导致问题更高版本上 （例如，您看到控制台输出中），并且还可能更难进行调试。

> [!NOTE]
> 在其中调用方法的情况下`null`值，`NullReferenceException`结果。 你通常想要避免使用`try/catch`阻止对于常规的异常，即，不依赖于特定的库函数的异常。 任何对象可能会引发`NullReferenceException`。 如果您不确定，请检查库函数的文档。

在调试过程中，它是很好的特定`assert`语句，直至你知道需要将它替换为实际代码修补程序。 让我们假设你决定用户可能会遇到应用程序的发行版中的异常。 在这种情况下，则必须重构代码以确保您的应用程序不会引发致命异常或导致其他一些错误。 因此，若要修复此代码，将以下代码：

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

通过使用此代码，满足你的代码要求并确保与记录`firstname`或`lastname`的值`null`不添加到的数据。

在此示例中，我们添加了两个`assert`循环内的语句。 通常情况下，使用时`assert`，则最好添加`assert`语句在函数或方法的入口点 （从开始）。 当前正在查看`UpdateRecords`示例应用程序中的方法。 在此方法中，您知道是否两个方法自变量的一个问题是`null`，因此请查看这两个与`assert`语句在函数的入口点。

```csharp
public static void UpdateRecords(List<User> db, User[] users)
{
    Debug.Assert(db != null);
    Debug.Assert(users != null);
```

对于上面的语句中，你的意图是加载现有数据 (`db`)，并检索新数据 (`users`) 之前更新的任何内容。

可以使用`assert`与任何类型的解析为的表达式`true`或`false`。 因此，例如，您可以添加`assert`如下语句。

```csharp
Debug.Assert(users[0].points > 0);
```

前面的代码是非常有用，如果你想要指定以下目的： 新的点值大于零 (0) 所需更新用户的记录。

## <a name="inspect-your-code-in-the-debugger"></a>检查你在调试器中的代码

好了，现在，修复了所有关键问题的示例应用的内容后，可以转到其他重要的东西 ！

我们向您介绍调试器的异常帮助器，但调试器是一个功能更为强大的工具，还可以执行其他操作，例如单步执行代码，检查其变量。 这些功能更强大的功能可在许多情况下，尤其是以下：

* 尝试将隔离运行时 bug 在代码中，但无法使用方法和先前讨论的工具完成此操作。

* 你想要验证你的代码，即，运行时对其以确保它是按预期方式运行，可以执行什么操作到观看它。

    是观看你的代码运行时对其有所帮助。 可以了解有关你的代码的详细信息这种方式，并在它们清单任何明显症状之前通常可以识别 bug。

若要了解如何使用调试器的基本功能，请参阅[零基础调试](../debugger/debugging-absolute-beginners.md)。

## <a name="fix-performance-issues"></a>修复性能问题

Bug 的另一种包括导致你的应用运行缓慢或占用大量内存的代码效率低下。 通常情况下，优化性能是更高版本在你的应用开发中做的事情。 但是，您可能会遇到性能问题早期 （例如，您看到您的应用程序的某个部分运行速度缓慢），可能需要进行早期测试使用分析工具对应用程序。 有关分析 CPU 使用率工具和内存分析器等工具的详细信息，请参阅[先来看一下分析工具](../profiling/profiling-feature-tour.md)。

## <a name="next-steps"></a>后续步骤

在本文中，已了解如何避免和修复代码中的许多常见 bug 以及何时使用调试器。 接下来，了解有关使用 Visual Studio 调试器以修复 bug 的详细信息。

> [!div class="nextstepaction"]
> [零基础调试](../debugger/debugging-absolute-beginners.md)
