---
title: 在 Unity 中使用 .NET 4.x
author: therealjohn
ms.author: johmil
ms.date: 08/29/2018
ms.topic: conceptual
ms.assetid: E2C9420F-A5D5-4472-9020-2B63FB27A133
ms.technology: vs-unity-tools
ms.workload:
- unity
ms.openlocfilehash: 0fb4560a196404687c60ce67f39b9c0754a24769
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71253146"
---
# <a name="using-net-4x-in-unity"></a>在 Unity 中使用 .NET 4.x

自 2002 年 Microsoft 最初发布更新以来，C# 和 .NET（Unity 脚本的基础技术）一直在不断更新。 但 Unity 开发者可能并未意识到 C# 语言和 .NET Framework 不断在添加新功能。 那是因为在 Unity 2017.1 之前，Unity 一直在使用与 .NET 3.5 等效的脚本运行时，已多年未进行更新。

随着 Unity 2017.1 的发布，Unity 引入了升级到 .NET 4.6、C# 6 兼容版本的实验版脚本运行时。 在 Unity 2018.1 中，与 .NET 4.x 等效的运行时不再视为实验版，较旧的等效于 .NET 3.5 的运行时现被视为旧版本。 随着 Unity 2018.3 的发布，Unity 计划将已升级的脚本运行时作为默认选择，并进一步更新为 C# 7。 有关此路线图的详细信息和最新更新，请阅读 Unity 的[博客文章](https://blogs.unity3d.com/2018/07/11/scripting-runtime-improvements-in-unity-2018-2/)或访问其[实验性脚本预览论坛](https://forum.unity.com/forums/experimental-scripting-previews.107/)。 与此同时，请查看以下部分，了解有关 .NET 4.x 脚本运行时现在可用的新功能的详细信息。

## <a name="prerequisites"></a>系统必备

* [Unity 2017.1 或更高版本](https://unity3d.com/)（建议使用 2018.2）
* [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

## <a name="enabling-the-net-4x-scripting-runtime-in-unity"></a>在 Unity 中启用 .NET 4.x 脚本运行时

若要启用 .NET 4.x 脚本运行时，请执行以下步骤：

1. 通过选择“Edit > Project Settings > Player”，在 Unity Inspector中打开 PlayerSettings  。

1. 在“Configuration”标题下，单击“Scripting Runtime Version”下拉列表，然后选择“.NET 4.x Equivalent”    。 系统会提示重启 Unity。

![选择 .NET 4.x 等效项](media/vstu_scripting-runtime-version.png)

## <a name="choosing-between-net-4x-and-net-standard-20-profiles"></a>在 .NET 4.x 和 .NET Standard 2.0 配置文件之间进行选择

一旦切换到 .NET 4.x 等效脚本运行时，可使用 PlayerSettings 中的下拉菜单指定“Api Compatibility Level”（“Edit > Project Settings > Player”）   。 有两种选项：

* **.NET Standard 2.0**。 此配置文件与 .NET Foundation 发布的 [.NET Standard 2.0 配置文件](https://github.com/dotnet/standard/blob/master/docs/versions/netstandard2.0.md)匹配。 Unity 建议新项目使用 .NET Standard 2.0。 它比 .NET 4.x 小，有利于尺寸受限的平台。 此外，Unity 承诺在 Unity 支持的所有平台上支持此配置文件。

* **.NET 4.x**。 此配置文件提供对最新 .NET 4 API 的访问权限。 它包括 .NET Framework 类库中提供的所有代码，并且支持 .NET Standard 2.0 配置文件。 如果 .NET Standard 2.0 配置文件中未包含项目所需的部分 API，请使用 .NET 4.x 配置文件。 但此 API 的某些部分并非在所有 Unity 平台上均受支持。

可在 Unity 的[博客文章](https://blogs.unity3d.com/2018/03/28/updated-scripting-runtime-in-unity-2018-1-what-does-the-future-hold/)中阅读有关这些选项的更多信息。

### <a name="adding-assembly-references-when-using-the-net-4x-api-compatibility-level"></a>使用 .NET 4.x API 兼容级别时添加程序集引用

在“API 兼容级别”下拉列表中使用 .NET Standard 2.0 设置时，将引用和使用 API 配置文件中的所有程序集  。 但是，在使用较大的 .NET 4.x 配置文件时，默认情况下不会引用 Unity 附带的某些程序集。 若要使用这些 API，必须手动添加程序集引用。 可在 Unity 编辑器安装的 MonoBleedingEdge/lib/mono 目录中查看 Unity 附带的程序集  ：

![MonoBleedingEdge 目录](media/vstu_monobleedingedge.png)

例如，如果使用的是 .NET 4.x 配置文件且希望使用 `HttpClient`，则必须为 System.Net.Http.dll 添加程序集引用。 如果没有它，编译器将报错，指示缺少程序集引用：

![缺少程序集引用](media/vstu_missing-reference.png)

每次打开 Unity 项目时 Visual Studio 都会为其重新生成 .csproj 和 .sln 文件。 因此，无法直接在 Visual Studio 中添加程序集引用，因为它们将在重新打开项目时丢失。 相反，必须使用名为 mcs.rsp 的特殊文本文件  ：

1. 在 Unity 项目的根Assets目录中创建名为 mcs.rsp 的新文本文件   。

1. 在空文本文件的第一行，输入：`-r:System.Net.Http.dll`，然后保存文件。 可将“System.Net.Http.dll”替换为可能缺少引用的任何包含的程序集。

1. 重启 Unity 编辑器。

## <a name="taking-advantage-of-net-compatibility"></a>利用 .NET 兼容性

除新的 C# 语法和语言功能外，.NET 4.x 脚本运行时还允许 Unity 用户访问与旧 .NET 3.5 脚本运行时不兼容的大量 .NET 包。

### <a name="add-packages-from-nuget-to-a-unity-project"></a>将包从 NuGet 添加到 Unity 项目

[NuGet](https://www.nuget.org/) 是适用于 .NET 的包管理器。 NuGet 已集成到 Visual Studio 中。 但是，Unity 项目需要一个特殊的过程来添加 NuGet 包。 这是因为当在 Unity 中打开项目时，会重新生成其 Visual Studio 项目文件，从而撤消必要的配置。 若要将 NuGet 中的包添加到 Unity 项目，请执行以下操作：

1. 浏览 NuGet 以查找要添加的兼容包（.NET Standard 2.0 或 .NET 4.x）。 此示例演示将 [Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/)（一种用于处理 JSON 的常见包）添加到 .NET Standard 2.0 项目中。

1. 单击“Download”按钮  ：

    ![“下载”按钮](media/vstu_nuget-download.png)

1. 找到已下载的文件，并将文件扩展名从 .nupkg 更改为 .zip   。

1. 在 zip 文件中，导航到 lib/netstandard2.0 目录并复制 Newtonsoft.Json.dll 文件   。

1. 在 Unity 项目的根 Assests 文件夹中，创建一个名为“Plugins”的新文件夹   。 Plugins是 Unity 中的特殊文件夹名称。 有关详细信息，请参阅 [Unity 文档](https://docs.unity3d.com/Manual/Plugins.html)。

1. 将 Newtonsoft.Json.dll 文件粘贴到 Unity 项目的“Plugins”目录中   。

1. 在 Unity 项目的“Assets”目录中创建名为 link.xml 的文件，并添加以下 XML   。  此操作将确保 Unity 的字节码去除过程在导出到 IL2CPP 平台时不会删除必要的数据。  虽然此步骤专用于此库，但在处理其他以类似方式使用反射的库时可能会遇到问题。  有关详细信息，请参阅有关此主题的 [Unity 文档](https://docs.unity3d.com/Manual/IL2CPP-BytecodeStripping.html)。

    ```xml
    <linker>
      <assembly fullname="System.Core">
        <type fullname="System.Linq.Expressions.Interpreter.LightLambda" preserve="all" />
      </assembly>
    </linker>
    ```

一切就绪后，现在可使用 Json.NET 包。

```csharp
using Newtonsoft.Json;
using UnityEngine;

public class JSONTest : MonoBehaviour
{
    class Enemy
    {
        public string Name { get; set; }
        public int AttackDamage { get; set; }
        public int MaxHealth { get; set; }
    }
    private void Start()
    {
        string json = @"{
            'Name': 'Ninja',
            'AttackDamage': '40'
            }";

        var enemy = JsonConvert.DeserializeObject<Enemy>(json);

        Debug.Log($"{enemy.Name} deals {enemy.AttackDamage} damage.");
        // Output:
        // Ninja deals 40 damage.
    }
}
```

这是不含依赖项的库的简单使用示例。 当 NuGet 包依赖于其他 NuGet 包时，需手动下载这些依赖项，并以相同方式将它们添加到项目中。

## <a name="new-syntax-and-language-features"></a>新的语法和语言功能

使用已更新的脚本运行时，Unity 开发者可访问 C# 6 以及一系列新的语言功能和语法。

### <a name="auto-property-initializers"></a>自动属性初始化表达式

在 Unity 的 .NET 3.5 脚本运行时中，自动属性语法可轻松快速定义未初始化的属性，但初始化必须在脚本的其他位置进行。 现在使用 .NET 4.x 运行时，可在同一行中初始化自动属性：

```csharp
// .NET 3.5
public int Health { get; set; } // Health has to be initialized somewhere else, like Start()

// .NET 4.x
public int Health { get; set; } = 100;
```

### <a name="string-interpolation"></a>字符串内插

使用较旧的 .NET 3.5 运行时，字符串串联需要繁琐的语法。 现在使用 .NET 4.x 运行时，[`$`字符串内插](https://docs.microsoft.com/dotnet/csharp/language-reference/tokens/interpolated)功能允许以更直接和可读的语法将表达式插入到字符串中：

```csharp
// .NET 3.5
Debug.Log(String.Format("Player health: {0}", Health)); // or
Debug.Log("Player health: " + Health);

// .NET 4.x
Debug.Log($"Player health: {Health}");
```

### <a name="expression-bodied-members"></a>Expression-Bodied 成员

使用 .NET 4.x 运行时中提供的新的 C# 语法，[Lambda 表达式](https://docs.microsoft.com/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)可替换函数主体，使它们更为简洁：

```csharp
// .NET 3.5
private int TakeDamage(int amount)
{
    return Health -= amount;
}

// .NET 4.x
private int TakeDamage(int amount) => Health -= amount;
```

还可以在只读属性中使用 expression-bodied 成员：

```csharp
// .NET 4.x
public string PlayerHealthUiText => $"Player health: {Health}";
```

### <a name="task-based-asynchronous-pattern-tap"></a>基于任务的异步模式 (TAP)

[异步编程](https://docs.microsoft.com/dotnet/csharp/async)允许执行耗时的操作，而不会导致应用程序无响应。 此功能还允许代码等待耗时的操作完成，然后继续执行取决于这些操作结果的代码。 例如，可等待文件加载或网络操作完成。

在 Unity 中，异步编程通常使用[协同程序](https://docs.unity3d.com/Manual/Coroutines.html)来完成。 但是，从 C# 5 开始，.NET 开发中异步编程的首选方法是[基于任务的异步模式 (TAP)](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap)，该方法将 `async` 和 `await` 关键字与 [System.Threading.Task](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task) 结合使用。 总之，在 `async` 函数中，可 `await`（等待）任务完成，同时不会阻止应用程序的其余部分更新：

```csharp
// Unity coroutine
using UnityEngine;
public class UnityCoroutineExample : MonoBehaviour
{
    private void Start()
    {
        StartCoroutine(WaitOneSecond());
        DoMoreStuff(); // This executes without waiting for WaitOneSecond
    }
    private IEnumerator WaitOneSecond()
    {
        yield return new WaitForSeconds(1.0f);
        Debug.Log("Finished waiting.");
    }
}
```

```csharp
// .NET 4.x async-await
using UnityEngine;
using System.Threading.Tasks;
public class AsyncAwaitExample : MonoBehaviour
{
    private async void Start()
    {
        Debug.Log("Wait.");
        await WaitOneSecondAsync();
        DoMoreStuff(); // Will not execute until WaitOneSecond has completed
    }
    private async Task WaitOneSecondAsync()
    {
        await Task.Delay(TimeSpan.FromSeconds(1));
        Debug.Log("Finished waiting.");
    }
}
```

TAP 是一个复杂的内容，具有相对于 Unity 的细微差别，这是开发人员应该斟酌的。 因此，TAP 不是 Unity 中协同程序的通用替代品，而是另一个可利用的工具。 此功能不属于本文范畴，但下方提供了一些通常的最佳做法和技巧。

#### <a name="getting-started-reference-for-tap-with-unity"></a>有关在 Unity 中使用 TAP 的入门参考

这些提示可帮助你开始在 Unity 中使用 TAP：

* 预期等待的异步函数应具有返回类型 [`Task`](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task) 或 [`Task<TResult>`](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task-1)。
* 返回任务的异步函数其名称后应附加后缀“Async”  。 “Async”后缀有助于指示需始终等待某个函数。
* 仅为从传统同步代码触发异步函数的函数使用 `async void` 返回类型。 无法等待此类函数，且不应在其名称中包含“Async”后缀。
* 默认情况下，Unity 使用 UnitySynchronizationContext 来确保异步函数在主线程上运行。 无法在主线程外部访问 Unity API。
* 可使用 [`Task.Run`](https://msdn.microsoft.com/library/hh195051.aspx) 和 [`Task.ConfigureAwait(false)`](https://msdn.microsoft.com/library/system.threading.tasks.task.configureawait.aspx) 等方法在后台线程上运行任务。 当从主线程移除成本高昂的操作以提高性能时，此技术非常有用。 但是，使用后台线程可能会导致发生难以调试的问题，例如[争用条件](https://wikipedia.org/wiki/Race_condition)。
* 无法在主线程外部访问 Unity API。
* Unity WebGL 生成不支持使用线程的任务。

#### <a name="differences-between-coroutines-and-tap"></a>协同程序和 TAP 之间的差异

协同程序和 TAP/async-await 之间存在一些重要差异：

* 协同程序无法返回值，但 `Task<TResult>` 可以。
* 无法将 `yield` 放置在 try-catch 语句中，因此使用协同程序处理错误十分困难。 但是，try-catch 适用于 TAP。
* Unity 的协程程序功能在不是从 MonoBehaviour 派生的类中不可用。 TAP 非常适合此类中的异步编程。
* 但 Unity 并不建议将 TAP 作为协同程序的整体替代项。 对于任何给定的项目，分析是了解一种方法相对于另一种方法的具体结果的唯一方法。

> [!NOTE]
> 截至 Unity 2018.2，不完全支持使用断点调试异步方法；但是，[Unity 2018.3 中预计会出现此功能](https://twitter.com/jbevain/status/900043560665235456)。

### <a name="nameof-operator"></a>nameof 运算符

`nameof` 运算符获取变量、类型或成员的字符串名称。 在某些情况下，使用 `nameof` 会很方便，包括记录错误、获取枚举的字符串名称：

```csharp
// Get the string name of an enum:
enum Difficulty {Easy, Medium, Hard};
private void Start()
{
    Debug.Log(nameof(Difficulty.Easy));
    RecordHighScore("John");
    // Output:
    // Easy
    // playerName
}
// Validate parameter:
private void RecordHighScore(string playerName)
{
    Debug.Log(nameof(playerName));
    if (playerName == null) throw new ArgumentNullException(nameof(playerName));
}
```

### <a name="caller-info-attributes"></a>调用方信息属性

[调用方信息属性](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/caller-information)提供有关方法调用方的信息。 必须为要与调用方信息属性一起使用的每个参数提供默认值：

```csharp
private void Start ()
    {
        ShowCallerInfo("Something happened.");
    }
    public void ShowCallerInfo(string message,
            [System.Runtime.CompilerServices.CallerMemberName] string memberName = "",
            [System.Runtime.CompilerServices.CallerFilePath] string sourceFilePath = "",
            [System.Runtime.CompilerServices.CallerLineNumber] int sourceLineNumber = 0)
    {
        Debug.Log($"message: {message}");
        Debug.Log($"member name: {memberName}");
        Debug.Log($"source file path: {sourceFilePath}");
        Debug.Log($"source line number: {sourceLineNumber}");
    }
// Output:
// Something happened
// member name: Start
// source file path: D:\Documents\unity-scripting-upgrade\Unity Project\Assets\CallerInfoTest.cs
// source line number: 10
```

### <a name="using-static"></a>Using static

[Using static](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/using-static) 允许使用静态函数，且无需键入其类名。 虽然此步骤专用于此库，但在处理其他以类似方式使用反射的库时可能会遇到问题

```csharp
// .NET 3.5
using UnityEngine;
public class Example : MonoBehaviour
{
    private void Start ()
    {
        Debug.Log(Mathf.RoundToInt(Mathf.PI));
        // Output:
        // 3
    }
}
```

```csharp
// .NET 4.x
using UnityEngine;
using static UnityEngine.Mathf;
public class UsingStaticExample: MonoBehaviour
{
    private void Start ()
    {
        Debug.Log(RoundToInt(PI));
        // Output:
        // 3
    }
}
```

## <a name="il2cpp-considerations"></a>IL2CPP 注意事项

将游戏导出到 iOS 等平台时，Unity 将使用其 IL2CPP 引擎将 IL“转换”为 C++ 代码，然后使用目标平台的本机编译器进行编译。 在此方案中，有几个不支持的 .NET 功能，例如反射的部分内容和使用 `dynamic` 关键字。 虽然可在自己的代码中使用这些功能，但使用第三方 DLL 和 SDK 时可能会遇到问题，这些 DLL 和 SDK 并非使用 Unity 和 IL2CPP 编写。 有关此主题的详细信息，请参阅 Unity 站点上的[脚本限制](https://docs.unity3d.com/Manual/ScriptingRestrictions.html)文档。

此外，如之前 Json.NET 示例中所述，Unity 将尝试在 IL2CPP 导出过程中裁剪掉未使用的代码。  虽然这通常不是问题，但对于使用反射的库，它可能会意外地删除在导出时无法确定是否被调用而在运行时可能被调用的属性或方法。  若要解决这些问题，请添加一个 link.xml 文件到项目中，该文件中包含的程序集和命名空间列表不会执行裁剪过程。   有关完整详细信息，请参阅[有关字节码裁剪的 Unity 文档](https://docs.unity3d.com/Manual/IL2CPP-BytecodeStripping.html)。

## <a name="net-4x-sample-unity-project"></a>.NET 4.x 示例 Unity 项目

该示例包含多个 .NET 4.x 功能的示例。 可在 [GitHub](https://github.com/Microsoft/unity-scripting-upgrade) 下载项目或查看源代码。

## <a name="additional-resources"></a>其他资源

* [Unity 博客 - Unity 2018.2 中的脚本运行时改进](https://blogs.unity3d.com/2018/07/11/scripting-runtime-improvements-in-unity-2018-2/)
* [C# 的历史记录](https://docs.microsoft.com/dotnet/csharp/whats-new/csharp-version-history)
* [C# 6 中的新增功能](https://docs.microsoft.com/dotnet/csharp/whats-new/csharp-6)
* [Unity 中的异步编程 - 使用协同程序和 TAP](https://blogs.msdn.microsoft.com/appconsult/2017/09/01/unity-coroutine-tap)
* [Unity 2017 使用 Async-Await 而非协同程序](http://www.stevevermeulen.com/index.php/2017/09/using-async-await-in-unity3d-2017/)
* [Unity 论坛 - 实验性脚本预览](https://forum.unity.com/forums/experimental-scripting-previews.107/)
