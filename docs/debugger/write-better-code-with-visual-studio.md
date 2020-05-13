---
title: 调试技术和工具
description: 使用 Visual Studio 修复异常、错误并改进代码，从而编写效果更佳、bug 更少的代码
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301019"
---
# <a name="debugging-techniques-and-tools-to-help-you-write-better-code"></a>有助于编写更佳代码的调试技术和工具

修复代码中的 bug 和错误这项工作非常耗时，有时甚至令人沮丧。 了解如何有效地调试是需要时间的，但 Visual Studio 这样功能强大的 IDE 可以大大降低这项工作的难度。 IDE 有助于更快速地修复错误和调试代码，不仅如此，它还有助于编写效果更佳、bug 更少的代码。 本文旨在帮助你从整体上了解“修复 bug”的过程，让你知道何时使用代码分析器、何时使用调试器、如何修复异常以及如何有目的地编写代码。 如果你已经知道需要使用调试器，请参阅[初探调试器](../debugger/debugger-feature-tour.md)。

本文讨论如何利用 IDE 提高编码过程的效率。 其中涉及几个任务，例如：

* 利用 IDE 的代码分析器准备要调试的代码

* 如何修复异常（运行时错误）

* 如何有目的地编码来最大程度减少 bug（使用断言）

* 何时使用调试器

为了演示这些任务，我们将展示尝试调试应用时最常遇到的一些错误和 bug 类型。 尽管示例代码为 C#，但概念性信息普遍适用于 C++、Visual Basic、JavaScript 和 Visual Studio 支持的其他语言（有标注处除外）。 屏幕截图为 C#。

## <a name="create-a-sample-app-with-some-bugs-and-errors-in-it"></a>创建一个包含 bug 和错误的示例应用

下面的代码包含一些 bug，可使用 Visual Studio IDE 进行修复。 这里的应用是一个简单应用，它模拟这样一个过程：从某个操作获取 JSON 数据，将该数据反序列化为对象，并使用新数据更新简单列表。

创建应用：

1. 必须安装 Visual Studio；根据要创建的应用类型，还必须安装“.NET Core 跨平台开发”或“.NET 桌面开发”工作负载   。

    如果尚未安装 Visual Studio，请转到  [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/) 页免费安装。

    如果需要安装工作负载但已安装 Visual Studio，请单击“工具” > “获取工具和功能”   。 Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”或“.NET Core 桌面开发”工作负载，然后选择“修改”    。

1. 打开 Visual Studio。

    ::: moniker range=">=vs-2019"
    在“开始”窗口上，选择“创建新项目”  。 在搜索框中键入“控制台”，然后选择“控制台应用(.NET Core)”或“控制台应用(.NET Framework)”    。 选择“下一步”  。 键入项目名称（如 Console_Parse_JSON），然后单击“创建”   。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件”   > “新建”   > “项目”  。 在“新建项目”对话框的左窗格中，在“Visual C#”下，选择“控制台应用”，然后在中间窗格中选择“控制台应用(.NET Core)”或“控制台应用(.NET Framework)”      。 键入名称（如 Console_Parse_JSON），然后单击“确定”   。
    ::: moniker-end

    如果没有看到“控制台应用(.NET Core)”或“控制台应用(.NET Framework)”项目模板，请转到“工具” > “获取工具和功能”，这会打开 Visual Studio 安装程序     。 选择“.NET Core 跨平台开发”或“.NET 桌面开发”工作负载，然后选择“修改”    。

    Visual Studio 创建控制台项目，该项目显示在右窗格的“解决方案资源管理器”中。

1. 将项目的“Program.cs”文件中的默认代码替换为下面的示例代码  。

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

## <a name="find-the-red-and-green-squiggles"></a>找到红色和绿色波浪线！

在尝试启动示例应用并运行调试器之前，请检查代码编辑器中的代码，查找红色和绿色波浪线。 它们表示由 IDE 的代码分析器识别到的错误和警告。 红色波浪线表示编译时错误，必须先修复这些错误，然后才能运行代码。 绿色波浪线表示警告。 虽然不修复警告通常也可以运行应用，但它们可能是导致 bug 的源头，对它们进行核查常常可以节省不少时间和麻烦。 如果你偏爱列表视图，也可以在“错误列表”窗口中显示这些警告和错误  。

在示例应用中，可以看到几条红色波浪线，表示需要修复问题，还有一条绿色波浪线，表示需要检查。 下面是第一个错误。

![用红色波浪线标示的错误](../debugger/media/write-better-code-red-squiggle.png)

若要修复此错误，需要借用 IDE 的另一项功能，该功能由灯泡图标表示。

## <a name="check-the-light-bulb"></a>查看灯泡图标！

第一条红色波浪线表示了一个编译时错误。 将鼠标悬停在它上面，可以看到消息 ```The name `Encoding` does not exist in the current context```。

请注意，此错误会在左下方显示一个灯泡图标。 灯泡图标![灯泡图标](../ide/media/light-bulb-icon.png)与螺丝刀图标![螺丝刀图标](../ide/media/screwdriver-icon.png)一起表示有助于修复或重构内联代码的快速操作。 灯泡表示应修复的问题  。 螺丝刀表示可以选择修复的问题。 单击左侧的“使用 System.Text”，使用第一个建议的修复来解决此错误  。

![使用灯泡修复代码](../debugger/media/write-better-code-missing-include.png)

单击此项时，Visual Studio 会将 `using System.Text` 语句添加到“Program.cs”文件的顶部  ，此时红色波浪线将消失。 （如果你不确定应使用哪一项建议的修复，请在应用修复之前选择右侧的“预览更改”链接。） 

上述错误很常见，通常可以通过在代码中添加新的 `using` 语句来解决。 有几个与此类似的常见错误，如 ```The type or namespace `Name` cannot be found.```这类错误可能表示缺少程序集引用（右键单击项目，选择“添加” > “引用”   ）、名称拼写错误，或需添加缺失的库（对于 C#，可右键单击项目并选择“管理 NuGet 包”以进行添加  ）。

## <a name="fix-the-remaining-errors-and-warnings"></a>修复剩余错误和警告

在此代码中，还有几条需要检查的波浪线。 在这里，可以看到一个常见的类型转换错误。 将鼠标悬停在波浪线上时，可以看到代码尝试将字符串转换为整数，但不支持这样做，除非添加显式代码来进行转换。

![类型转换错误](../debugger/media/write-better-code-conversion-error.png)

由于代码分析器不能估计出你的意图，因此目前没有灯泡可帮助你解决这一问题。 若要修复此错误，你需要了解代码的意图。 在此示例中，不难看出 `points` 应为数值（整数），因为你是要将 `points` 添加到 `totalpoints`。

若要修复此错误，请将 `User` 类的 `points` 成员从：

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

接下来，将鼠标悬停在 `points` 数据成员的声明中的绿色波浪线上。 代码分析器将显示未对该变量进行赋值。

![未赋值变量的警告消息](../debugger/media/write-better-code-warning-message.png)

通常，这表示需要修复的问题。 但是，在示例应用中，实际上是在反序列化过程中将数据存储在 `points` 变量中，然后将该值添加到 `totalpoints` 数据成员。 在此示例中，你知道代码的意图，因此可以放心地忽略该警告。 但是，如果想要消除此警告，可以将以下代码：

```csharp
item.totalpoints = users[i].points;
```

替换为以下内容：

```csharp
item.points = users[i].points;
item.totalpoints += users[i].points;
```

绿色波浪线消失。

## <a name="fix-an-exception"></a>修复异常

如果已修复所有红色波浪线表示的问题，并解决（或者至少核查了）所有绿色波浪线表示的问题，就可以启动调试器并运行应用了。

按 F5  （“调试”>“开始调试”  ）或调试工具栏中的“开始调试”  按钮![开始调试](../debugger/media/dbg-tour-start-debugging.png "开始调试")。

此时，示例应用引发 `SerializationException` 异常（运行时错误）。 这表示，应用无法正常处理其尝试序列化的数据。 因为是在调试模式下启动的应用（附加调试器），因此调试器的异常帮助程序会直接转到引发异常的代码，并提供有用的错误消息。

![发生 SerializationException](../debugger/media/write-better-code-serialization-exception.png)

错误消息表明 `4o` 值无法分析为整数。 因此，在此示例中，你知道数据有缺陷：`4o` 应为 `40`。 但是，如果实际情况下数据不由你控制（假设你从 Web 服务中获取数据），该怎么做呢？ 如何解决此问题？

遇到异常时，你需要提出（并解答）几个问题：

* 此异常只是你可以修复的 bug 吗？ 或者，

* 你的用户可能遇到此异常吗？

如果是前者，修复该 bug 即可。 （在示例应用中，即修复有缺陷的数据。）如果是后者，则可能需要使用 `try/catch` 块处理代码中的异常（我们将在下一节中介绍其他可用的策略）。 在示例应用中，将以下代码：

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

`try/catch` 块会降低性能，因此尽量只在必要情况下才使用它们，即下面两种情况：(a) 它们可能出现在应用的发行版中；(b) 方法文档指示你检查该异常（假定文档已经完善！）。 在许多情况下，你都可以适当地处理异常，不让用户察觉。

下面是有关异常处理的几个重要提示：

* 避免使用空 catch 块，例如 `catch (Exception) {}`，它不会采取适当的操作来显示或处理错误。 空的或无信息的 catch 块可能隐藏异常，它不能使代码调试变简单，反而会使它变得更难。

* 在引发异常的特定函数（示例应用中为 `ReadObject`）周围使用 `try/catch` 块。 如果在更大的代码块中使用它，则最终将隐藏错误的位置。 例如，不要在对父函数 `ReadToObject` 的调用周围使用 `try/catch` 块（如此处所示），否则你将不知道异常发生的确切位置。

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

* 对于在应用中添加的你不熟悉的功能，尤其是与外部数据交互的功能（例如 Web 请求），请参阅文档以查看该功能可能引发哪些异常。 对于正确的错误处理和应用调试来说，这可能是至关重要的信息。

对于示例应用，通过将 `4o` 更改为 `40` 来修复 `GetJsonData` 方法中的 `SerializationException`。

## <a name="clarify-your-code-intent-by-using-assert"></a>使用断言阐明代码意图

单击调试工具栏中的“重启”![重启应用](../debugger/media/dbg-tour-restart.png "重启应用")按钮 (Ctrl + Shift + F5)     。 这样可以以更少的步骤重启应用。 控制台窗口中会显示以下输出。

![输出中的 null 值](../debugger/media/write-better-code-using-assert-null-output.png)

你可以在此输出中发现一些错误。 第三条记录的“name”和“lastname”为空   ！

下面介绍一种有用但通常未被充分利用的编码做法，即在函数中使用 `assert` 语句。 添加以下代码，可包含运行时检查以确保 `firstname` 和 `lastname` 不为 `null`。 将 `UpdateRecords` 方法中的以下代码：

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

在开发过程中向函数添加类似的 `assert` 语句，可以帮助指定代码的意图。 在上面的示例中，我们指定了以下内容：

* 需要有效的字符串来表示名字
* 需要有效的字符串来表示姓氏

以这种方式指定意图，可以强制实施要求。 这是一种简单便捷的方法，可用于在开发期间显示 bug。 （还可以使用 `assert` 语句作为单元测试中的主要元素。）

单击调试工具栏中的“重启”![重启应用](../debugger/media/dbg-tour-restart.png "重启应用")按钮 (Ctrl + Shift + F5)     。

> [!NOTE]
> `assert` 代码仅在调试版本中有效。

重新启动时，调试器会在 `assert` 语句上暂停，因为表达式 `users[i].firstname != null` 的计算结果为 `false` 而不是 `true`。

![断言解析为 false](../debugger/media/write-better-code-using-assert.png)

`assert` 错误表明存在需要核查的问题。 `assert` 可以涵盖许多不一定会出现异常的情况。 在此示例中，用户不会看到异常，会将 `null` 值添加为记录列表中的 `firstname`。 这可能会导致以后出现问题（例如在控制台输出中所看到的），并且可能使调试难度增大。

> [!NOTE]
> 对 `null` 值调用方法时，将生成 `NullReferenceException`。 通常情况下，应避免用 `try/catch` 块调试一般异常，即与特定库函数无关的异常。 任何对象都可能引发 `NullReferenceException`。 如果不确定，请查看库函数的文档。

在调试过程中，最好保留特定的 `assert` 语句，直到你确定需要将其替换为实际的代码修复。 假设你确定用户在应用的发布版本中可能遇到某个异常。 在这种情况下，必须重构代码，确保你的应用不会引发严重异常或导致其他错误。 那么，为了修复此代码，请将以下代码：

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

使用此代码，可以满足代码要求，确保未将 `firstname` 或 `lastname` 值为 `null` 的记录添加到数据中。

在此示例中，我们在一个循环中添加了两个 `assert` 语句。 通常，在使用 `assert` 时，最好在函数或方法的入口点（开始处）添加 `assert` 语句。 你现在看到的是示例应用中的 `UpdateRecords` 方法。 在此方法中，如果任意一方法参数为 `null`，就必定会出现问题，因此，请在函数入口点处使用 `assert` 语句检查这两个参数。

```csharp
public static void UpdateRecords(List<User> db, User[] users)
{
    Debug.Assert(db != null);
    Debug.Assert(users != null);
```

对于上述语句，你的意图是在更新任何数据之前加载现有数据 (`db`) 并检索新数据 (`users`)。

可以将 `assert` 用于可解析为 `true` 或 `false` 的任何类型的表达式。 例如，可以添加类似如下的 `assert` 语句。

```csharp
Debug.Assert(users[0].points > 0);
```

如果要指定以下意图，则上述代码将很有用：需要具有大于零 (0) 的新分数值，才更新用户的记录。

## <a name="inspect-your-code-in-the-debugger"></a>在调试器中检查代码

好了，既然你已修复示例应用的所有关键错误和异常，可以继续处理其他重要内容了！

我们展示了调试器的异常帮助程序，但调试器工具的强大功能远不止于此，你还可以利用它执行其他操作，例如单步执行代码并检查其变量。 这些更强大的功能适用于多种情况，特别是以下几种：

* 你正在尝试隔离代码中的运行时 bug，但无法使用前面讨论过的方法和工具来执行此操作。

* 你想验证代码，即在代码运行时对其进行观察，以确保其行为符合预期。

    在代码运行时对其进行监视具有指导意义。 通过这种方式，你可以更深入地了解代码，并且常可在出现明显征兆之前识别 bug。

若要了解如何使用调试器的基本功能，请参阅[零基础调试](../debugger/debugging-absolute-beginners.md)。

## <a name="fix-performance-issues"></a>修复性能问题

另一种类型的 bug 包括会导致应用程序运行缓慢或使用过多内存的低效代码。 优化性能通常在应用开发的后期进行。 但是，你可能会提前遇到性能问题（例如发现应用的某些部分运行缓慢），这时就可能需要尽早通过分析工具来测试应用。 有关分析工具（例如 CPU 使用情况工具和内存分析器）的详细信息，请参阅[首先查看分析工具](../profiling/profiling-feature-tour.md)。

## <a name="next-steps"></a>后续步骤

本文介绍了如何避免和修复代码中的许多常见错误以及何时使用调试器。 接下来，可以详细了解如何使用 Visual Studio 调试器修复 bug。

> [!div class="nextstepaction"]
> [零基础调试](../debugger/debugging-absolute-beginners.md)
