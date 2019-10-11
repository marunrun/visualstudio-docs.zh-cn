---
title: 调试技术和工具
description: 使用 Visual Studio 修复异常、修复错误并改进代码，编写更好的代码，使代码更少
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
ms.openlocfilehash: b1fe0a9bb1e966bd1451bb5d816eaab814071fb5
ms.sourcegitcommit: 7825d4163e52d724e59f6c0da209af5fbef673f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72000175"
---
# <a name="debugging-techniques-and-tools-to-help-you-write-better-code"></a>有助于编写更好代码的调试技术和工具

修复代码中的 bug 和错误可能是一项非常耗时的任务，有时会使任务更难。 请花些时间来了解如何有效调试，但功能强大的 IDE （如 Visual Studio）会使您的工作变得更加轻松。 IDE 可以帮助您更快速地修复错误和调试代码，而不只是这样做，但它还可帮助您编写更好的代码，但 bug 更少。 本文旨在为您提供 "修复 bug" 过程的整体视图，因此您将知道何时使用代码分析器、何时使用调试器、如何修复异常以及如何为意向编写代码。 如果已知道需要使用调试器，请参阅[第一次查看调试器](../debugger/debugger-feature-tour.md)。

本文讨论如何利用 IDE 提高编码会话的工作效率。 我们接触几项任务，例如：

* 利用 IDE 的代码分析器准备要调试的代码

* 如何修复异常（运行时错误）

* 如何通过为意向编码来最大程度地减少 bug （使用断言）

* 何时使用调试器

为了演示这些任务，我们将显示一些最常见的错误类型和错误，并在尝试调试应用时遇到错误。 尽管示例代码为C#，但概念信息通常适用于C++、Visual Basic、JavaScript 和 Visual Studio 支持的其他语言（注明的情况除外）。 屏幕截图为 C#。

## <a name="create-a-sample-app-with-some-bugs-and-errors-in-it"></a>创建一个示例应用，其中包含一些错误和错误

下面的代码具有一些可使用 Visual Studio IDE 进行修复的 bug。 此处的应用程序是一个简单的应用，它模拟从某个操作获取 JSON 数据、将数据反序列化到对象，以及使用新数据更新简单列表。

创建应用：

1. 打开 Visual Studio，然后选择 " **File** > **New** > "**项目**。 在 **" C#视觉对象**" 下，选择 " **Windows 桌面**" 或 " **.net Core**"，然后在中间窗格中选择一个**控制台应用**。

    > [!NOTE]
    > 如果没有看到“控制台应用程序”项目模板，请单击“新建项目”对话框左侧窗格中的“打开 Visual Studio 安装程序”链接。 Visual Studio 安装程序启动。 选择“.NET Core 桌面开发”或“.NET Core 跨平台开发”工作负载，然后选择“修改”。

2. 在 "**名称**" 字段中，键入**Console_Parse_JSON** ，然后单击 **"确定"**。 Visual Studio 随即创建项目。

3. 将项目的*Program.cs*文件中的默认代码替换为下面的示例代码。

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

## <a name="find-the-red-and-green-squiggles"></a>找到红色和绿色波形曲线！

在尝试启动示例应用并运行调试器之前，请检查代码编辑器中的代码中是否有红色和绿色波形曲线。 这表示由 IDE 的代码分析器标识的错误和警告。 红色波形曲线是编译时错误，必须先修复这些错误，然后才能运行代码。 绿色波形曲线是警告。 虽然你可以在不修复警告的情况下运行应用程序，但它们可能是 bug 的源，你通常通过调查它们来节省时间和麻烦。 如果你更喜欢列表视图，则这些警告和错误还会显示在 "**错误列表**" 窗口中。

在示例应用中，你会看到多个需要修复的红色波形曲线，还有一个要查看的绿色。 下面是第一个错误。

![显示为红色波形曲线的错误](../debugger/media/write-better-code-red-squiggle.png)

若要修复此错误，您将看到 IDE 的另一项功能，该功能由灯泡图标表示。

## <a name="check-the-light-bulb"></a>检查灯泡！

第一个红色波形曲线表示编译时错误。 将鼠标悬停在它上方，你会看到消息 ```The name `Encoding` does not exist in the current context```。

请注意，此错误会向左下方显示一个灯泡图标。 除了螺丝钉图标 ![screwdriver icon @ no__t），灯泡图标 ![light 灯泡图标 @ no__t 表示可帮助你修复或重构代码内联的快速操作。 灯泡表示*应*修复的问题。 螺丝钉是为了解决问题，您可以选择解决这些问题。 使用第一个建议的修复方法，单击左侧的 "**使用 System. 文本**" 解决此错误。

![使用灯泡修复代码](../debugger/media/write-better-code-missing-include.png)

单击此项时，Visual Studio 会将 `using System.Text` 语句添加到*Program.cs*文件的顶部，红色波浪线将消失。 （如果不确定建议的解决方法，请在应用修补程序之前选择右侧的 "**预览更改**" 链接。）

前面的错误是通常通过向代码添加新的 `using` 语句来修复的常见错误。 这种错误有几个常见的类似错误，如 ```The type or namespace `Name` cannot be found.``` 这类错误可能表示缺少程序集引用（右键单击项目，选择 "**添加** > **引用**"）、拼写错误的名称或缺少所需的库若要添加（ C#对于，右键单击项目并选择 "**管理 NuGet 包**"）。

## <a name="fix-the-remaining-errors-and-warnings"></a>修复剩余错误和警告

在此代码中，还有几个波形曲线。 在这里，你会看到一个常见的类型转换错误。 当你将鼠标悬停在波形曲线上时，你会看到代码尝试将字符串转换为 int，这不受支持，除非你添加显式代码来进行转换。

![类型转换错误](../debugger/media/write-better-code-conversion-error.png)

由于代码分析器不能猜到你的意图，因此没有任何轻型电灯泡来帮助你解决这一问题。 若要修复此错误，您需要了解代码的意图。 在此示例中，很难看到 `points` 应为数值（整数）值，因为您尝试将 @no__t 添加到 `totalpoints`。

若要修复此错误，请将 @no__t 类的 @no__t 成员从此：

```csharp
[DataMember]
internal string points;
```

更改为：

```csharp
[DataMember]
internal int points;
```

代码编辑器中的红色波浪线将消失。

接下来，将鼠标悬停在 `points` 数据成员的声明中的绿色波形曲线上。 代码分析器告诉您变量从未赋值。

![未赋值变量的警告消息](../debugger/media/write-better-code-warning-message.png)

通常，这表示需要修复的问题。 但是，在示例应用中，实际上是在反序列化过程中将数据存储在 `points` 变量中，然后将该值添加到 @no__t 数据成员中。 在此示例中，您知道代码的目的，可以安全地忽略该警告。 但是，如果想要消除此警告，可以替换以下代码：

```csharp
item.totalpoints = users[i].points;
```

替换为以下内容：

```csharp
item.points = users[i].points;
item.totalpoints += users[i].points;
```

绿色曲线会消失。

## <a name="fix-an-exception"></a>修复异常

如果已修复所有红色波形曲线并解决了此情况，或者至少调查了所有绿色波形曲线，则可以启动调试器并运行应用。

按 F5（“调试”>“开始调试”）或调试工具栏中的“开始调试”按钮（![开始调试](../debugger/media/dbg-tour-start-debugging.png "Start Debugging")）。

此时，示例应用引发 `SerializationException` 异常（运行时错误）。 也就是说，应用会对尝试序列化的数据进行浅压浅。 由于已在调试模式下启动应用（附加调试器），因此调试器的异常帮助器会直接转到引发异常的代码，并提供有用的错误消息。

![发生 SerializationException](../debugger/media/write-better-code-serialization-exception.png)

错误消息指示不能将值 `4o` 作为整数来分析。 因此，在此示例中，您知道数据是错误的： `4o` 应 `40`。 但是，如果您不是实际情况中的数据控制（假设您从 web 服务中获取了数据），您该怎么做呢？ 如何解决此问题？

遇到异常时，您需要询问（并回答）几个问题：

* 此异常是否只是您可以解决的 bug？ 或者，

* 您的用户可能会遇到这种异常情况吗？

如果是前者，请修复该错误。 （在示例应用中，这意味着修复错误的数据。）如果是后者，则您可能需要使用 `try/catch` 块处理代码中的异常（我们在下一节中介绍其他可能的策略）。 在示例应用中，替换以下代码：

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

@No__t-0 块具有一定的性能开销，因此你只需在你真正需要它们时使用它们，即，在应用的发布版本中可能出现的位置（a），并且该方法的文档指示你应检查是否存在异常（如suming 文档已完成！）。 在许多情况下，您可以适当地处理异常，用户永远不需要知道。

下面是有关异常处理的几个重要提示：

* 避免使用空 catch 块（例如 `catch (Exception) {}`），该 catch 块不采取适当的措施来公开或处理错误。 空或不信息 catch 块可以隐藏异常，并使代码更难以调试，而不是更容易。

* 在引发异常的特定函数周围使用 `try/catch` 块（在示例应用中 `ReadObject`）。 如果在更大的代码块中使用它，则会结束隐藏错误的位置。 例如，不要在对父 @no__t 函数的调用中使用 `try/catch` 块（如此处所示），也不会确切知道发生异常的位置。

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

* 对于包含在应用中的不熟悉的函数（特别是与外部数据的交互（如 web 请求），请查看文档以查看函数可能引发哪些异常。 这可能是正确的错误处理和调试应用程序的关键信息。

对于示例应用，通过将 @no__t 更改为 `4o` 来修复 @no__t 方法中的 @no__t 0。

## <a name="clarify-your-code-intent-by-using-assert"></a>使用 assert 阐明代码意向

单击调试工具栏中的“重启”![重启应用](../debugger/media/dbg-tour-restart.png "RestartApp")按钮 (Ctrl + Shift + F5)。 这更少的步骤会重启应用。 控制台窗口中显示以下输出。

![输出中的 Null 值](../debugger/media/write-better-code-using-assert-null-output.png)

你可以在此输出中看到不是很正确的内容。 第三个记录的**名称**和**姓氏**为空白！

这是一种很好的时机，就是一种很好的做法，那就是使用函数中的 `assert` 语句，这种做法通常是使用不足的。 通过添加以下代码，你可以包括运行时检查，以确保 `firstname` 和 @no__t 不 `null`。 替换 `UpdateRecords` 方法中的以下代码：

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

通过在开发过程中向函数添加如下所示的 `assert` 语句，可以帮助指定代码的意图。 在前面的示例中，我们将指定以下内容：

* 第一个名称需要有效的字符串
* 最后一个名称需要有效的字符串

通过以这种方式指定意向，可以强制实施要求。 这是一种简单便捷的方法，可用于在开发期间显示 bug。 （`assert` 语句也用作单元测试中的主要元素。）

单击调试工具栏中的“重启”![重启应用](../debugger/media/dbg-tour-restart.png "RestartApp")按钮 (Ctrl + Shift + F5)。

> [!NOTE]
> @No__t-0 代码仅在调试版本中处于活动状态。

重新启动时，调试器会在 `assert` 语句上暂停，因为表达式 `users[i].firstname != null` 的计算结果为 `false` 而不是 `true`。

![断言解析为 false](../debugger/media/write-better-code-using-assert.png)

@No__t-0 错误表明存在需要调查的问题。 `assert` 可以涵盖许多不一定会出现异常的情况。 在此示例中，用户将看不到异常，并将 `null` 值作为记录列表中 `firstname` 添加。 这可能会导致以后出现问题（例如，在控制台输出中看到），并且可能更难调试。

> [!NOTE]
> 在对 `null` 值调用方法的情况下，会生成 @no__t 结果。 通常，应避免将 `try/catch` 块用于一般例外，即不依赖于特定库函数的异常。 任何对象都可以引发 `NullReferenceException`。 如果不确定，请查看库函数的文档。

在调试过程中，最好保留特定的 `assert` 语句，直到你知道需要将其替换为实际的代码修复。 假设你确定用户在应用的发布版本中可能会遇到异常。 在这种情况下，你必须重构代码，以确保你的应用不会引发异常或导致其他错误。 因此，若要修复此代码，请替换以下代码：

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

通过使用此代码，你可以满足你的代码要求，并确保不向数据中添加 @no__t 为0或 @no__t 为1的记录 `null`。

在此示例中，我们在一个循环中添加了两个 `assert` 语句。 通常，在使用 `assert` 时，最好在函数或方法的入口点（开始）添加 @no__t 1 语句。 你当前正在查看示例应用中的 @no__t 0 方法。 在此方法中，如果其中一个方法参数 @no__t 为-0，您就会遇到问题，因此，请在函数的入口点使用 @no__t 1 语句同时检查它们。

```csharp
public static void UpdateRecords(List<User> db, User[] users)
{
    Debug.Assert(db != null);
    Debug.Assert(users != null);
```

对于上述语句，你的目的是在更新任何数据之前加载现有数据（`db`）并检索新数据（`users`）。

可以将 `assert` 与可解析为 @no__t 或 @no__t 2 的任意类型的表达式一起使用。 例如，你可以添加类似于下面的 `assert` 语句。

```csharp
Debug.Assert(users[0].points > 0);
```

如果要指定以下目的，则上述代码将很有用：更新用户的记录需要大于零（0）的新点值。

## <a name="inspect-your-code-in-the-debugger"></a>在调试器中检查代码

好了，既然您已经修复了所有错误的应用程序，您可以转到其他重要内容吧！

我们向您展示了调试器的异常帮助程序，但调试器是一个功能强大的工具，它还允许您执行其他操作，如逐句通过代码并检查其变量。 这些功能更强大的功能在许多情况下都很有用，特别是：

* 你正在尝试隔离代码中的运行时 bug，但无法使用前面讨论过的方法和工具来执行此操作。

* 要验证代码，即在运行代码时对其进行监视，以确保其行为符合预期并执行所需的操作。

    在代码运行时，请对其进行监视。 您可以通过这种方式了解您的代码的详细信息，并经常确定 bug，然后再确定任何明显的症状。

若要了解如何使用调试器的基本功能，请参阅[为绝对初学者调试](../debugger/debugging-absolute-beginners.md)。

## <a name="fix-performance-issues"></a>修复性能问题

其他类型的错误包括导致应用程序运行缓慢或使用过多内存的低效代码。 通常，在应用程序开发中，可以优化性能。 但是，你可以及早地遇到性能问题（例如，你会看到应用程序的某些部分运行缓慢），并且你可能需要在早期通过分析工具来测试应用程序。 有关分析工具（例如 CPU 使用情况工具和内存分析器）的详细信息，请参阅[分析工具](../profiling/profiling-feature-tour.md)。

## <a name="next-steps"></a>后续步骤

本文介绍了如何在代码中避免和修复许多常见错误以及何时使用调试器。 接下来，详细了解如何使用 Visual Studio 调试器修复 bug。

> [!div class="nextstepaction"]
> [零基础调试](../debugger/debugging-absolute-beginners.md)
