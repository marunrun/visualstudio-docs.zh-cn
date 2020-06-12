---
title: 更改日志（Visual Studio Tools for Unity、Windows）| Microsoft Docs
ms.custom: ''
ms.date: 5/19/2020
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: ea490b7e-fc0d-44b1-858a-a725ce20e396
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: cc1cbc98d4612c8f480cca0a9469d4a56da10bb3
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84184778"
---
# <a name="change-log-visual-studio-tools-for-unity-windows"></a>更改日志（Visual Studio Tools for Unity、Windows）

Visual Studio Tools for Unity 更改日志。

## <a name="4610"></a>4.6.1.0
发布日期：2020 年 5 月 19 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 如果无法在 Unity 端创建消息服务器，则会发出警告。
  
  - 在轻量级编译期间正确运行分析器。
  
  - 修复了从 UPE 创建的 MonoBehaviour 类与文件名称不匹配的问题。

## <a name="4600"></a>4.6.0.0
发布时间：2020 年 4 月 14 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对 CodeLens（Unity 脚本和消息）的支持。
  
  - 添加了 [`UNT0012`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0012.md) 诊断。 在 `StartCoroutine()` 中检测并包装对协同例程的调用。

  - 添加了 [`UNT0013`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0013.md) 诊断。 检测并删除无效或冗余的 `SerializeField` 属性。

  - 添加了 [`UNT0014`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0014.md) 诊断。 检测用非组件或非接口类型调用的 `GetComponent()`。
  
  - 为 `IDE0051` 添加了 [`USP0009`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0009.md) 抑制器。 请勿将具有 `ContextMenu` 属性的方法或由具有 `ContextMenuItem` 属性的字段引用的方法标记为未使用。

  - 为 `IDE0051` 添加了 [`USP0010`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0010.md) 抑制器。 请勿将具有 `ContextMenuItem` 属性的字段标记为未使用。
  
  - 为 `IDE0044` 添加了 [`USP0011`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0011.md) 抑制器。 请勿将具有 `ContextMenuItem` 属性的字段设为只读字段。
  
  - [`USP0004`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0004.md)、[`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0006.md) 和 [`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0007.md) 现在都适用于 `SerializeReference` 和 `SerializeField` 属性。
  
### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 当编辑器能够进行通信时，才向 Unity 发送启动/停止命令。
  
  - 修复了与继承消息相关的 QuickInfo 文档。
  
  - 修复了 `CreateInspectorGUI` 消息的消息范围。

  - 请勿报告与具有多态修饰符的方法相关的 [`UNT0001`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0001.md)。

- **评估版：**

  - 修复了别名为 using 的处理。

## <a name="4510"></a>4.5.1.0

发布日期：2020 年 3 月 16 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 为 `IDE0051` 添加了 [`USP0008`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0008.md) 抑制器。 与 Invoke、InvokeRepeating、StartCoroutine 或 StopCoroutine 一起使用的专用方法不应标记为未使用。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了 OnDrawGizmos/OnDrawGizmosSelected 文档。

- **评估版：**

  - 修复了 Lambda 参数检查。

## <a name="4501"></a>4.5.0.1

发布日期：2020 年 2 月 19 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了针对错误的消息签名的 [`UNT0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0006.md) 诊断检查。 当检查具有多个继承级别的类型时，此诊断可能会失败，并显示以下消息：`warning AD0001: Analyzer 'Microsoft.Unity.Analyzers.MessageSignatureAnalyzer' threw an exception of type 'System.ArgumentException' with message 'An item with the same key has already been added`。

## <a name="4500"></a>4.5.0.0

发布日期：2020 年 1 月 22 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对 HLS 文件的支持。
  
  - 为 `IDE0051` 添加了 [`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0006.md) 抑制器。 具有 `SerializeField` 属性的专用字段不应标记为未使用。
  
  - 为 `CS0649` 添加了 [`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0007.md) 抑制器。 具有 `SerializeField` 属性的字段不应标记为未分配。  

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了项目生成问题（无法始终正确找到 `GenerateTargetFrameworkMonikerAttribute` 目标）。

## <a name="4420"></a>4.4.2.0

发布时间：2019 年 12 月 3 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了使用用户定义的接口进行的诊断。

  - 修复了表达式格式错误的快速工具提示。

## <a name="4410"></a>4.4.1.0

发布时间：2019 年 11 月 6 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对 Unity 后台进程的支持。 （调试程序能够自动连接到主进程，而不是子进程）。
  
  - 为 Unity 消息添加了快速工具提示，可显示关联的文档。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 使用高级二进制和 invocation 表达式修复了标签比较分析器 [`UNT0002`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0002.md)。

### <a name="deprecated-features"></a>弃用的功能

- **集成：**

  - 展望未来，Visual Studio Tools for Unity 将仅支持 Visual Studio 2017+。

## <a name="4400"></a>4.4.0.0

发布时间：2019 年 10 月 15 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 为所有 Unity 消息的 `IDE0060`（未使用的参数）添加了 [`USP0005`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0005.md) 抑制器。
  
  - 为标有 `TooltipAttribute` 的字段添加了快速工具提示。 （这也适用于使用此字段的简单 get 访问器）。

## <a name="4330"></a>4.3.3.0

发布日期：2019 年 9 月 23 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了轻量级版本的错误和警告报告。

## <a name="4320"></a>4.3.2.0

发布日期：2019 年 9 月 16 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 通过添加特定于 Unity 的新诊断，深化了 Visual Studio 对 Unity 项目的理解。 还通过取消不适用于 Unity 项目的一般 C# 诊断，使 IDE 更智能。 例如，IDE 不会显示将检查器变量更改为 `readonly` 的快速修复，因此这会阻止你修改 Unity 编辑器中的变量。
    - [`UNT0001`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0001.md)：即使 Unity 消息为空，运行时也会调用它们，请勿声明它们，以避免 Unity 运行时进行不必要的处理。
    - [`UNT0002`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0002.md)：使用字符串相等比较标记的速度比内置的 CompareTag 方法慢。
    - [`UNT0003`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0003.md)：为了获得类型安全性，最好使用 GetComponent 的通用形式。
    - [`UNT0004`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0004.md)：更新消息依赖于帧速率，应使用 Time.deltaTime 而不是 Time.fixedDeltaTime。
    - [`UNT0005`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0005.md)：固定更新消息与帧速率无关，应使用 Time.fixedDeltaTime 而不是 Time.deltaTime。
    - [`UNT0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0006.md)：检测到此 Unity 消息的方法签名不正确。
    - [`UNT0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0007.md)：Unity 重写与 null 合并不兼容的 Unity 对象的 null 比较运算符。
    - [`UNT0008`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0008.md)：Unity 重写与 null 传播不兼容的 Unity 对象的 null 比较运算符。
    - [`UNT0009`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0009.md)：将 InitializeOnLoad 特性应用于类时，需要提供静态构造函数。 InitializeOnLoad 特性可确保在编辑器启动时调用该函数。
    - [`UNT0010`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0010.md)：应只使用 AddComponent() 创建 MonoBehaviours。 MonoBehaviour 是一个组件，需要附加到 GameObject。
    - [`UNT0011`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/UNT0011.md)：应只使用 CreateInstance() 创建 ScriptableObject。 ScriptableObject 需要由 Unity 引擎创建，才能处理 Unity 消息方法。
    - 针对 `IDE0029` 的 [`USP0001`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0001.md)：Unity 对象不应使用 Null 合并。
    - 针对 `IDE0031` 的 [`USP0002`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0002.md)：Unity 对象不应使用 Null 传播。
    - 针对 `IDE0051` 的 [`USP0003`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0003.md)：Unity 消息由 Unity 运行时调用。
    - 针对 `IDE0044` 的 [`USP0004`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/master/doc/USP0004.md)：不应将具有 SerializeField 特性的字段设为只读。

## <a name="4310"></a>4.3.1.0

发布日期：2019 年 9 月 4 日

### <a name="new-features"></a>新增功能

- **评估版：**

  - 添加了对更佳类型显示的支持，即 `List<object>`，而不是 `List'1[[System.Object, <corlib...>]]`。

  - 添加了对指针成员访问的支持，即 `p->data->member`。

  - 添加了对数组初始值设定项中的隐式转换的支持，即 `new byte [] {1,2,3,4}`。

## <a name="4300"></a>4.3.0.0

发布日期：2019 年 8 月 13 日

### <a name="new-features"></a>新增功能

- **调试器：**

  - 增加了对 MDS 协议 2.51 的支持。

- **集成：**

  - 改进了“附加到 Unity 实例”窗口的排序、搜索和刷新功能。 现在甚至为本地播放机显示 PID（通过查询系统上的侦听套接字以检索拥有的进程）。

  - 增加了对 asmdef 文件的支持。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了与 Unity 播放器通信时格式错误消息的处理。

- **评估版：**

  - 修复了表达式中命名空间的处理。

  - 修复了 IntPtr 类型的检测。
  
  - 修复了出现异常的单步执行问题。

  - 修复了伪标识符（如 $exception）计算问题。

  - 防止在取消引用无效地址时出现故障。  

  - 修复了已卸载的 appdomains 的问题。

## <a name="4201"></a>4.2.0.1

发布时间：2019 年 7 月 24 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了一个新选项，可从 Unity 项目资源管理器创建任意类型的文件。
  
  - 改进了在对 Unity 项目使用快速生成时的诊断缓存。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了文件扩展名不是由任何已知编辑器处理的问题。

  - 修复了对 Unity 项目资源管理器中自定义扩展的支持。

  - 修复了在主对话框外保存设置的问题。

  - 删除了旧的 Microsoft.VisualStudio.MPF 依赖项。

## <a name="4110"></a>4.1.1.0

发布日期：2019 年 5 月 24 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 已将 MonoBehaviour API 更新到 2019.1。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 启用轻型生成时，修复了要输出的报告警告和错误。

  - 修复了轻型生成性能。

## <a name="4100"></a>4.1.0.0

发布日期：2019 年 5 月 21 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对新的批处理 API 的支持以更快地重新加载项目。

  - 禁用了 Unity 项目的完整生成，取而代之的是使用 IntelliSense 错误和警告。 事实上，Unity 使用表示 Unity 内部所执行操作的类库项目创建 Visual Studio 解决方案。 尽管如此，Visual Studio 中的生成结果从未由 Unity 使用或选取，因为其编译管道已关闭。 在 Visual Studio 中生成只是使用资源。 如果由于你具有工具或依赖于完整生成的安装程序而需要完整生成，则可以禁用此优化（工具/选项/Tools for Unity/禁用项目的完整生成）。

  - 加载 Unity 项目时自动显示 Unity 项目资源管理器 (UPE)。 UPE 将停靠在解决方案资源管理器旁边。

  - 使用 2019.x 更新了项目名称提取机制。

  - 添加了对 UPE 中的 Unity 包的支持。 只有引用包（使用 `Packages` 文件夹中的 manifest.json）和本地包（嵌入在 `Packages` 文件夹中）是可见的。

- **Project Generation:**

  - 处理解决方案文件时，请保留外部属性。

- **评估版：**

  - 添加了对别名限定名称的支持（目前仅支持全局命名空间）。 因此，表达式计算器现在正在使用 global::namespace.type 窗体接受类型。

  - 添加了对 `pointer[index]` 窗体的支持，在语义上等同于指针取消引用 `*(pointer+index)` 窗体。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了 Microsoft.VisualStudio.MPF 的依赖项问题。

  - 修复了 UWP 播放器附加，而无需加载任何项目。

  - 尚未附加 Visual Studio 时修复了自动资产数据库刷新。

  - 修复了标签和复选框的主题问题。

- **调试器：**

  - 使用静态构造函数修复了单步执行。

## <a name="4005"></a>4.0.0.5

发布时间：2019 年 2 月 27 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了安装包的 Visual Studio 版本检测问题。

  - 删除了安装包中未使用的程序集。

## <a name="4004"></a>4.0.0.4

发布时间：2019 年 2 月 13 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 增加了对安装过程中正确检测 Unity 进程，并允许安装引擎更好地处理文件锁的支持。

  - 更新了 `ScriptableObject` API。

## <a name="4003"></a>4.0.0.3

发布时间：2019 年 1 月 31 日

### <a name="new-features"></a>新增功能

- **Project Generation:**

  - 公共字段和序列化字段将不再引发警告。 在创建这些消息的 Unity 项目中，我们自动禁止了 `CS0649` 和 `IDE0051` 编译器警告。

- **集成：**

  - 改进了显示 Unity 编辑器和播放器实例的用户体验（现可调整窗口大小、使用统一边距并显示大小调整手柄）。 添加了 Unity 编辑器的进程 ID 信息。

  - 更新了 `MonoBehaviour` API。

- **评估版：**

  - 增加了对本地函数的支持。

  - 增加了对伪变量（异常和对象标识符）的支持。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了名字对象图像和主题的问题。

  - 仅在自动刷新资产数据库时，在调试期间写入到输出窗口。

  - 修复了 MonoBehaviour 向导筛选的 UI 延迟。

- **调试器：**

  - 修复了在使用旧协议版本时读取命名参数的自定义属性。

## <a name="4002"></a>4.0.0.2

发布时间：2019 年 1 月 23 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了实验性生成版本生成。

  - 修复了项目文件事件处理，以最小化 UI 线程压力。

  - 修复了成批文本更改的完成提供程序。

- **调试器：**

  - 修复了附加调试器的用户调试消息显示问题。

## <a name="4001"></a>4.0.0.1

发布时间：2018 年 12 月 10 日

### <a name="new-features"></a>新增功能

- **评估版：**

  - 将 NRefactory 替换为 Roslyn 以进行表达式计算。

  - 添加了对指针的支持：取消引用、强制转换和指针算法（为此同时需要 Unity 2018.2+ 和新运行时）。

  - 添加了对数组指针视图（例如在 C++ 中）的支持。 需要一个指针表达式，然后追加一个逗号和要查看的元素数。

  - 添加了对异步构造的支持。

- **集成：**

  - 添加了对保存时自动刷新 Unity 资产数据库的支持。 这在默认情况下处于启用状态，当在 Visual Studio 中保存脚本时，将在 Unity 端触发重新编译。 保存时可以在“工具\选项\适用于 Unity 的工具\刷新 Unity 的 AssetDatabase”中禁用此功能。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了 Visual Studio 未被选为首选的外部编辑器时的桥激活。

  - 修复了表达式格式不正确或不受支持的表达式计算。

## <a name="4000"></a>4.0.0.0

发布时间：2018 年 12 月 4 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对 Visual Studio 2019 的支持（必须至少为 Unity 2018.3 才能将 Visual Studio 2019 用作外部脚本编辑器）。

  - 采用了 Visual Studio 图像服务和目录，同时完全支持 HDPI 缩放、像素完美的图像和主题。

### <a name="deprecated-features"></a>弃用的功能

- **集成：**

  - 展望未来，Visual Studio Tools for Unity 将仅支持 Unity 5.2+（带有 Unity 内置的 Visual Studio 集成）。

  - 展望未来，Visual Studio Tools for Unity 将仅支持 Visual Studio 2015+。

  - 删除了旧版语言服务、错误列表和状态栏。

  - 删除了 Quick Monobehaviour 向导（以支持专用的 intellisense 支持）。

## <a name="3903"></a>3.9.0.3

发布时间：2018 年 11 月 28 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 已修复：添加或删除第一个项目中的脚本时，项目会重新加载，及 intellisense 问题。

## <a name="3902"></a>3.9.0.2

发布时间：2018 年 11 月 19 日

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了用于与 Unity 调试器引擎进行通信的库中的死锁，此死锁会导致 Visual Studio 或 Unity 冻结，尤其是在用户点击“附加到 Unity”或重启游戏时。

## <a name="3901"></a>3.9.0.1

发布时间：2018 年 11 月 15 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了选中另一个默认编辑器时 Unity 插件的激活。

## <a name="3900"></a>3.9.0.0

发布时间：2018 年 11 月 13 日

### <a name="bug-fixes"></a>Bug 修复

- **Project Generation:**

  - 回滚了针对 Unity 性能缺陷的解决方案（此缺陷已由 Unity 修复）。

## <a name="3807"></a>3.8.0.7

发布时间：2018 年 9 月 20 日

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - （从 3.9.0.2 版向后移植）修复了用于与 Unity 调试器引擎进行通信的库中的死锁，此死锁会导致 Visual Studio 或 Unity 冻结，尤其是在用户点击“附加到 Unity”或重启游戏时。

## <a name="3806"></a>3.8.0.6

发布日期：2018 年 8 月 27 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了项目和解决方案的重载。

## <a name="3805"></a>3.8.0.5

发布时间：2018 年 8 月 20 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了监视订阅处置的项目。

## <a name="3804"></a>3.8.0.4

发布时间：2018 年 8 月 14 日

### <a name="new-features"></a>新增功能

- **评估版：**

  - 添加了对指针值的支持。

  - 添加了对泛型方法的支持。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 在多个项目更改的情况下智能重载。

## <a name="3803"></a>3.8.0.3

发布时间：2018 年 7 月 24 日

### <a name="bug-fixes"></a>Bug 修复

- **Project Generation:**

  - （从 3.9.0.0 版向后移植）回滚了针对 Unity 性能缺陷的解决方案（此缺陷已由 Unity 修复）。

## <a name="3802"></a>3.8.0.2

发布时间：2018 年 7 月 7 日

### <a name="bug-fixes"></a>Bug 修复

- **Project Generation:**

  - Unity 性能 Bug 的暂时解决方法：生成项目时缓存 MonoIsland。

## <a name="3801"></a>3.8.0.1

发布时间：2018 年 6 月 26 日

### <a name="new-features"></a>新增功能

- **调试：**

  - 添加了对 UserLog 和 UserBreak 命令的支持。

  - 添加了对延迟加载的支持（优化了网络负载和调试程序响应延迟）。

### <a name="bug-fixes"></a>Bug 修复

- **评估版：**

  - 改进了二元运算符表达式计算和方法搜索。

## <a name="3800"></a>3.8.0.0

发布时间：2018 年 5 月 30 日

### <a name="new-features"></a>新增功能

- **调试：**

  - 现支持在异步构造中显示变量。

  - 现支持在设置断点时处理嵌套类型以防止编译器构造出现警告。

- **集成：**

  - 现支持着色器的 textmate 语法（Shader 代码着色不再需要 C++ 工作负载）。

### <a name="bug-fixes"></a>Bug 修复

- **Project Generation:**

  - 使用新版 Unity 运行时，不要再将可移植 pdb 转换为 mdb。

## <a name="3701"></a>3.7.0.1

发布时间：2018 年 5 月 7 日

### <a name="bug-fixes"></a>Bug 修复

- **安装程序：**

  - 使用实验性生成时修复了依赖项问题。

## <a name="3700"></a>3.7.0.0

发布时间：2018 年 5 月 7 日

### <a name="new-features"></a>新增功能

- **调试：**

  - 增加了对安排的调试的支持（使用相同的 Visual Studio 会话调试多个播放器/编辑器）。

  - 增加了对 Android USB 播放器调试的支持。

  - 增加了对 UWP/IL2CPP 播放器调试的支持。

- **评估版：**

  - 增加了对十六进制说明符的支持。

  - 改进了监视窗口评估体验。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了异常设置的使用情况。

- **Project Generation:**

  - 从生成中排除包管理器编译单位。

## <a name="3605"></a>3.6.0.5

发布时间：2018 年 3 月 13 日

### <a name="new-features"></a>新增功能

- **Project Generation:**

  - 添加了对 Unity 2018.1 中新项目生成器的支持。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复处理自定义项目损坏状态方面的问题。

- **调试器：**

  - 修复了设置下一语句方面的问题。

## <a name="3604"></a>3.6.0.4

发布时间：2018 年 3 月 5 日

### <a name="bug-fixes"></a>Bug 修复

- **Project Generation:**

  - 修复了 Mono 版本检测的问题。

- **集成：**

  - 修复了 2018.1 和插件激活的计时问题。

## <a name="3603"></a>3.6.0.3

发布时间：2018 年 2 月 23 日

### <a name="new-features"></a>新增功能

- **Project Generation:**

  - 添加了对 .NET Standard 的支持。

### <a name="bug-fixes"></a>Bug 修复

- **Project Generation:**

  - 修复了 Unity 目标框架检测的问题。

- **调试器：**

  - 修复了用户代码外部引发的异常中断的问题。

## <a name="3602"></a>3.6.0.2

发布时间：2018 年 2 月 7 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 更新 UnityMessage API 接口 2017.3。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 仅对外部更改重载项目（含有限制）。

## <a name="3601"></a>3.6.0.1

发布时间：2018 年 1 月 24 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 固定自动 pdb 到 mdb 调试符号转换。

  - 修复了在尝试更改数组大小时对 EditorPrefs.GetBool 的间接调用影响检查器的问题。

## <a name="3600"></a>3.6.0.0

发布时间：2018 年 1 月 10 日

### <a name="new-features"></a>新增功能

- **Project Generation:**

  - 添加了对 2018.1 MonoIsland 引用模型的支持。

- **评估版：**

  - 添加了对 $exception 标识符的支持。

- **调试器：**

  - 添加了对含有新 Unity 运行时的 DebuggerHidden/DebuggerStepThrough 属性的支持。

- **向导：**

  - 引入向导的“最新”版本。

### <a name="bug-fixes"></a>Bug 修复

- **Project Generation:**

  - 修复了播放器项目的项目 GUID 计算。

- **调试器：**

  - 修复了处理突发事件的争用问题。

- **向导：**

  - 在插入方法前刷新 roslyn 上下文。

## <a name="3503"></a>3.5.0.3

发布时间：2018 年 1 月 9 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 固定自动 pdb 到 mdb 调试符号转换。

## <a name="3502"></a>3.5.0.2

发布时间：2017 年 12 月 4 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 从 Unity 添加或删除脚本时，Unity 项目现在会在 Visual Studio 中自动重载。

- **调试器：**

  - 增加了使用由 Xamarin 和 Visual Studio for Mac 共享的 Mono 调试程序选项，用于调试 Unity 编辑器。

  - 增加了对可移植调试符号文件的支持。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了安装依赖项问题。

  - 修复了 Unity API 帮助菜单未显示问题。

- **Project Generation:**

  - 修复了在处理后端为 IL2CPP/.NET 4.6 的 UWP 游戏时玩家项目的生成问题。

  - 修复了额外 .dll 扩展名错误添加到程序集文件问题。

  - 修复了使用特定项目 API 兼容级别而非全局兼容问题。

  - 不强制 AllowAttachedDebuggingOfEditor Unity，因为现在默认为“true”。

## <a name="3402"></a>3.4.0.2

发布时间：2017 年 9 月 19 日

### <a name="new-features"></a>新增功能

- **Project Generation:**

  - 添加了对 assembly.json 编译单元的支持。

  - 停止将 Unity 程序集复制到项目文件夹。

- **调试器：**

  - 添加了对使用新的 Unity 运行时设置下一个语句的支持。

  - 添加了对使用新的 Unity 运行时的十进制类型的支持。

  - 添加了对隐式/显式转换的支持。

### <a name="bug-fixes"></a>Bug 修复

- **评估版：**

  - 修复了使用隐式大小的数组创建。

  - 修复了编译器使用局部变量生成的项。

- **Project Generation:**

  - 修复了对 4.6 API 级别的 Microsoft.CSharp 的引用。

## <a name="3302"></a>3.3.0.2

发布时间：2017 年 8 月 15 日

### <a name="bug-fixes"></a>Bug 修复

- **Project Generation:**

  - 修复了 Unity 5.5 及更低版本上 Visual Studio 解决方案的生成问题。

## <a name="3300"></a>3.3.0.0

发布时间：2017 年 8 月 14 日

### <a name="new-features"></a>新增功能

- **评估版：**

  - 添加了对使用新的 Unity 运行时创建结构的支持。

  - 添加了对指针的极简支持。

### <a name="bug-fixes"></a>Bug 修复

- **评估版：**

  - 修复了基元上的方法调用。

  - 修复了其类型标记为 BeforeFieldInit 的字段评估。

  - 修复了具有二进制运算符（减）的不受支持的调用。

  - 修复了将项目添加到 Visual Studio Watch 时出现的问题。

- **Project Generation:**

  - 修复了使用 mcs.rsp 文件的程序集名称引用。

  - 修复了通过 API 级别进行定义的问题。

## <a name="3200"></a>3.2.0.0

发布时间：2017 年 5 月 10 日

### <a name="new-features"></a>新增功能

- **安装程序：**

  - 添加了对清除的 MEF 缓存的支持。

### <a name="bug-fixes"></a>Bug 修复

- **代码编辑器：**

  - 修复了自定义特性的分类/完成。

  - 修复 Unity 消息闪烁的问题。

## <a name="3100"></a>3.1.0.0

发布时间：2017 年 4 月 7 日

### <a name="new-features"></a>新增功能

- **调试器：**

  - 增加了对新的 Unity 运行时（与 .NET 4.6/C# 6 兼容）的支持。

- **Project Generation:**

  - 添加了对 .NET 4.6 配置文件的支持。

  - 添加了对 mcs.rsp 文件的支持。

  - 使用 Unity 5.6 时，始终启用不安全编译开关。

  - 使用 Windows 应用商店平台和 il2cpp 后端时，增加了对“Player”项目生成的支持。

### <a name="bug-fixes"></a>Bug 修复

- **代码编辑器：**

  - 使用自动完成功能修复了插入方法后的插入符号位置。

- **Project Generation:**

  - 删除了程序集版本后处理。

## <a name="3001"></a>3.0.0.1

发布时间：2017 年 3 月 7 日

### <a name="this-version-includes-all-new-features-and-bug-fixes-introduced-with-28x-series"></a>此版本包括 2.8.x 系列引入的所有新功能和 Bug 修复。

## <a name="2820---30-preview-3"></a>2.8.2.0 - 3.0 预览版 3
发布时间：2017 年 1 月 25 日

### <a name="bug-fixes"></a>Bug 修复

- **项目生成：**

  - 修复了两次引用插件项目（首次为二进制 DLL，然后为项目引用）方面的性能退化问题。

## <a name="2810---30-preview-2"></a>2.8.1.0 - 3.0 预览版 2
发布时间：2017 年 1 月 23 日

### <a name="bug-fixes"></a>Bug 修复

- **代码编辑器：**

  - 修复了在未以大括号完成的情况下启动属性声明时出现的崩溃问题。

- **调试器：**

  - 在新的 Unity 编译器/运行时下使用协同程序修复了函数断点。

  - 添加了针对不可绑定断点的情况（即找不到对应的源位置时）的警告。

- **Project Generation:**

  - 修复了包含特殊/本地化字符的 csproj 生成。

  - 修复了资产之外的引用，例如 Facebook SDK 等库。

- **杂项：**

  - 添加了针对防止 Unity 在安装或卸载时运行的检查。

  - 切换到了 https 以面向远程 Unity 文档。

## <a name="2800---30-preview"></a>2.8.0.0 - 3.0 预览版
发布时间：2016 年 11 月 17 日

### <a name="new-features"></a>新增功能

- **常规：**

  - 添加了 Visual Studio 2017 安装程序支持。

  - 添加了 Visual Studio 2017 扩展支持。

  - 添加了本地化支持。

- **代码编辑器：**

  - 添加了 Unity 消息的 C# IntelliSense。

  - 添加了 Unity 消息的 C# 代码着色功能。

- **调试器：**

  - 添加了对 `is`、`as`、直接强制转换、`default` 和 `new` 表达式的支持。

  - 添加了对字符串 concat 表达式的支持。

  - 添加了对十六进制显示整数值的支持。

  - 添加了对新建临时变量（语句）的支持。

  - 添加了对隐式基元转换的支持。

  - 改进了在需要或找不到某类型时显示的错误消息。

- **Project Generation:**

  - 删除了项目名称中的 CSharp 后缀。

  - 删除了对系统范围内 msbuild 目标文件的引用。

- **向导：**

  - 添加了对非行为类型（如编辑器或 EditorWindow）中 Unity 消息的支持。

  - 切换到了 Roslyn 以插入 Unity 消息并设置其格式。

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了在评估泛型类型时出现 Unity 故障的 bug。

  - 修复了处理可为 null 的类型方面的问题。

  - 修复了枚举处理方面的问题。

  - 修复了嵌套成员类型处理方面的问题。

  - 修复了集合索引器访问问题。

  - 修复了对使用新 C# 编译器调试迭代器框架的支持问题。

- **Project Generation:**

  - 修复了在面向 Unity Web Player 时阻止编译的 bug。

  - 修复了在使用 Web 编码的文件名编译脚本时阻止编译的 bug。

## <a name="2300"></a>2.3.0.0

发布时间：2016 年 7 月 14 日

### <a name="new-features"></a>新增功能

- **常规：**

  - 添加了在 Visual Studio 错误列表中禁用 Unity 控制台日志的选项。

  - 添加了允许修改生成的项目属性的选项。

- **调试器：**

  - 添加了文本、XML、HTML 和 JSON 字符串可视化工具。

- **向导：**

  - 添加了缺少的 MonoBehavior。

### <a name="bug-fixes"></a>Bug 修复

- **常规：**

  - 修复了与 ReSharper 间的冲突，该工具阻止 Visual Studio 设置中的控件显示。

  - 修复了与 Xamarin 间的冲突，该工具在某些情况下阻止调试。

- **调试器：**

  - 修复了导致 Visual Studio 在调试时冻结的问题。

  - 修复了 Visual Studio 2015 中函数断点的问题。

  - 修复了多个表达式计算问题。

## <a name="2200"></a>2.2.0.0

发布时间：2016 年 2 月 4 日

### <a name="new-features"></a>新增功能

- **向导：**

  - 在“实现 MonoBehavior”  向导中添加智能搜索。

  - 使向导区分上下文；例如，仅当使用 NetworkBehavior 时，NetworkBehavior 消息才可用。

  - 在向导中添加了对 NetworkBehavior 消息的支持。

- **UI：**

  - 添加了用于配置 MonoBehavior 消息可见性的选项。

  - 删除了与 Unity 项目不相关的 Visual Studio 属性页。

### <a name="bug-fixes"></a>Bug 修复

- **项目生成：**

  - 修复了在 Unity 4.6 上对 UnityEngine 和 UnityEditor 的引用。

  - 修复了 Unity 在 OSX 上运行时项目文件的生成。

  - 修复了对包含井号 (#) 字符的项目名称的处理。

  - 将生成的项目限制到了 C# 4。

- **调试器：**

  - 修复了在 Unity 协同程序内进行调试时表达式计算的问题。

  - 修复了导致 Visual Studio 在调试时冻结的问题。

- **UI：**

  - 修复了与 [Tabs Studio](https://tabsstudio.com/) Visual Studio 扩展的不兼容问题。

- **安装程序：**

  - 支持通过创建 HKLM 注册表项对 VSTU 进行计算机范围的安装（为所有用户安装）。

  - 修复了针对多个不同版本的 Visual Studio 安装相同版本的 VSTU 时卸载 VSTU 的问题。 例如，同时安装了 VSTU **2015** 2.1.0.0 和 VSTU **2013** 2.1.0.0 的情况。

## <a name="2100"></a>2.1.0.0

发布时间：2015 年 9 月 8 日

### <a name="new-features"></a>新增功能

- 支持 Unity 5.2

### <a name="bug-fixes"></a>Bug 修复

- 在低于 Unity 4.2 的版本中显示菜单项

- 当 Visual Studio 锁定 XML intellisense 文件时，不再显示错误消息。

- 当条件参数不是布尔值时处理 <\<When Changed>> 条件断点。

- 修复对 Windows 应用商店应用的 UnityEngine 和 UnityEditor 程序集的引用。

- 已修复在调试器中单步执行时的错误：无法单步执行，一般异常。

- 修复了 Visual Studio 2015 中的命中次数断点。

## <a name="2000"></a>2.0.0.0

发布时间：2015 年 7 月 20 日

### <a name="bug-fixes"></a>Bug 修复

- **Unity 集成：**

  - 修复了导入一个 DLL 和其调试符号 (PDB) 时使用 Visual Studio 2015 创建的调试符号的转换。

  - 当导入一个 DLL 和其调试符号 (PDB) 时，始终生成 MDB 文件，同时提供了 MDB 文件的情况除外。

  - 修复了带有 obj 目录的 Unity 项目目录的污染。

  - 修复了对 System.Xml.Link 和 System.Runtime.Serialization 的引用的代。

  - 添加了对项目文件生成 API 挂钩的多个订户的支持。

  - 即使锁定了一个要生成的文件，也应始终完成项目文件生成。

  - 当指定要包含在 C# 项目中的文件时，在扩展筛选器中添加了对 * 通配符的支持。

- **Visual Studio 集成：**

  - 修复了 Productivity Power Tools 的兼容性问题。

  - 修复了围绕事件和委托声明生成 MonoBehaviors。

- **调试器：**

  - 修复了调试时可能发生的冻结。

  - 修复了关于在特定堆栈帧中不显示局部变量的问题。

  - 修复了检查空数组。

## <a name="1990---20-preview-2"></a>1.9.9.0 - 2.0 预览版 2
发布时间：2015 年 4 月 2 日

### <a name="new-features"></a>新增功能

- **Unity 项目资源管理器：**

  - 重命名 Unity 项目资源管理器中的文件时将自动重命名类（请参阅“选项”  对话框）。

  - 在 Unity 项目资源管理器中自动选择新创建的脚本。

  - 跟踪 Unity 项目资源管理器中的活动脚本（请参阅“选项”  对话框）。

  - 双同步 Visual Studio 解决方案资源管理器（请参阅“选项”  对话框）。

  - 在 Unity 项目资源管理器中采用 Visual Studio 图标。

- **调试器：**

  - 从已保存或最近使用过的调试目标的列表中选择活动调试目标（请参阅“选项”  对话框）。

  - 在 MonoBehavior 方法上创建函数断点，并将它们应用于多个 MonoBehavior 类。

  - 在调试器中支持创建对象 ID。

  - 在调试器中支持断点命中次数。

  - 在调试器中支持异常时中断（实验。 请参阅“选项”  对话框）。

  - 在调试器中计算表达式时，支持对象和数组的创建。

  - 在调试器中计算表达式时，支持 Null 比较。

  - 筛选出调试器监视窗口中的过时成员。

- **安装程序：**

  - 优化 Visual Studio Tools for Unity 扩展注册。

  - 为 Unity 5 安装 Visual Studio Tools for Unity 包。

- **文档：** 改善文档生成的性能。

- **向导：** 支持适用于 Unity 4.6 和 Unity 5 的新 MonoBehavior 方法。

- **Unity：** 在项目文件生成过程中查找 .rsp 文件中的不安全标志和自定义定义。

- **UI：** Visual Studio 中已添加的 Visual Studio Tools for Unity“选项”对话框。

### <a name="bug-fixes"></a>Bug 修复

- **Unity 项目资源管理器：**

  - 从 Visual Studio 解决方案资源管理器移动或重命名文件后，刷新 Unity 项目资源管理器。

  - 重命名 Unity 项目资源管理器中的文件时，保留选择。

  - 防止在 Unity 项目资源管理器中双击时文件自动展开和折叠。

  - 确保新选择的文件在 Unity 项目资源管理器中可见。

- **调试器：**

  - 在调试器中计算表达式时，防止可能发生的 Visual Studio 冻结。

  - 确保方法调用发生在调试器中正确的域上。

- **Unity：**

  - 使用 Unity 5 更正 UnityVS.OpenFile 的位置。

  - 使用 Unity 5 更正 pdb2mdb 的位置。

  - 防止在项目文件生成过程中可能发生的异常。

  - 防止在 OSX 上运行 Unity 时可能发生的冻结。

  - 处理内部异常。

  - 将 Unity 控制台日志发送到 VS 错误列表。

- **文档：** 更正新 unity 文档的文档生成。

- **项目：** 需要时移动和重命名 Unity .meta 文件（甚至在文件夹中）。

- **向导：** 生成代码时更正 MonoBehavior 方法参数的顺序。

- **UI：** 支持 Visual Studio 主题的上下文菜单和图标。

## <a name="1980---20-preview"></a>1.9.8.0 - 2.0 预览版
发布时间：2014 年 11 月 12 日

### <a name="new-features"></a>新增功能

- 对 Visual Studio 2015 的支持。

- Visual Studio 2015 中 Unity 着色器的代码着色功能。

- 调试时改进的值的可视化效果：

  - ArrayList、列表、哈希表和词典更好的可视化。

  - 将非公共成员和静态成员显示为监视视图和局部视图中的类别。

  - 改进了 Unity 的 SerializedProperty 的显示，以仅评估对该属性有效的值字段。

  - DebuggerDisplayAttribute 支持类和结构。

  - DebuggerTypeProxyAttribute 支持。

- 请使用向导插入 MonoBehaviour 方法，以遵守用户编码约定。

- 在 UnityVS 生成的项目中实现对“编译时文本模板”的支持。

- 在 UnityVS 生成的项目中实现对 ResX 资源的支持。

- 支持在 Visual Studio 中打开 Unity 中的着色器。

### <a name="bug-fixes"></a>Bug 修复

- 当 Visual Studio 中的“附加和播放”触发后，请于在 Unity 中开始游戏前清除套接字。 使用“附加和播放”时，这会修复 Unity 和 VS 之间的一些连接稳定性问题。

- 避免调用 Unity 脚本引擎调试器界面中容易冻结 Unity 的方法。 附加调试器时，这将修复 Unity 冻结这一问题。

- 修复在无符号可用时调用堆栈的显示。

- 如果没有必要，则无需注册日志回调。

## <a name="1920"></a>1.9.2.0

发布时间：2014 年 10 月 9 日

### <a name="new-features"></a>新增功能

- 改进对 Unity 播放器的检测。

- 使用文件打开工具时，使 Unity 传递行号以及文件名。

- 如果没有本地文档，则默认为联机的 Unity 文档。

### <a name="bug-fixes"></a>Bug 修复

- 修复在重新加载域后命中断点时的潜在 Unity 故障。

- 修复在重新加载域后关闭“配置”或“关于”窗口时 Unity 控制台中显示的异常。

- 修复对本地运行的 64 位 Unity 的检测。

- 修复向导中每个 Unity 版本的 MonoBehaviour 筛选。

- 修复如果扩展名筛选器为空，则在项目文件中包含所有资产这一 bug。

## <a name="1910"></a>1.9.1.0

发布时间：2014 年 9 月 22 日

### <a name="new-features"></a>新增功能

- 优化将断点绑定到源位置的断点绑定。

- 在调试器的表达式计算中支持重载方法。

- 支持调试器的表达式计算中的装箱基元和值类型。

- 支持在调试匿名方法时重新创建 C# 局部变量环境。

- 从 Visual Studio 删除或重命名文件时，删除和重命名 .meta 文件。

### <a name="bug-fixes"></a>Bug 修复

- 修复 Visual Studio 主题的处理。 之前，黑色主题中的对话框可能会显示为空。

- 修复当连接调试器同时 Unity 进行重新编译时发生的 Unity 冻结。

- 调试在另一个系统编译的远程编辑器或播放器时，修复断点。

- 命中断点时修复可能的 Visual Studio 崩溃。

- 修复断点绑定，以避免断点显示为未加载。

- 修复调试器中变量范围的处理，以避免出现的实时变量超出范围。

- 修复在调试器的表达式计算中静态成员的查找。

- 修复调试器的表达式计算中的类型显示，以显示静态字段和属性。

- 修复 Unity 项目名称包含 Visual Studio 禁止的特殊字符时解决方案的生成（连接问题 #948666）。

- 修复 Visual Studio Tools Unity 包，以立即停止在取消选中选项后发送控制台事件（连接问题 #933357）。

- 修复引用检测，以正确地重新生成对新 API（如 UnityVS 生成的项目中的 UnityEngine.UI）的引用。

- 修复安装程序，以要求在安装前关闭 Visual Studio，从而避免损坏安装。

- 修复安装程序，以便将 Unity 引用程序集作为在所有版本的 VSTU 之间共享的适当独立组件进行安装。

- 修复在 64 位版本 Unity 中使用 VSTU 打开脚本的问题。

## <a name="1900"></a>1.9.0.0

发布时间：2014 年 7 月 29 日

### <a name="new-features"></a>新增功能

- 在“附加 Unity 调试器”窗口中，添加输入自定义 IP 和待调试端口的功能。

- 添加设置 Unity 是否在后台运行的配置选项。

- 添加生成解决方案和项目文件或仅生成项目文件的配置选项。

- 启动目标：选择“附加到 Unity”或“附加到 Unity 并播放”。

- 显示调试器中的多维数组。

- 处理新的 Unity 播放器调试端口。

- 处理对新 Unity 程序集（如 Unity 4.6 GUI 程序集）的引用。

- 调试时，解构闭包以正确显示局部变量。

- 调试时，将生成的迭代器变量解构到参数中。

- 重新加载项目后，保留 Unity 项目资源管理器的状态。

- 添加命令以使 Unity 项目资源管理器和当前的文档同步。

### <a name="bug-fixes"></a>Bug 修复

- 修复在启动调试器之前设置了条件的条件断点。

- 修复对 UnityEngine 的引用，以避免警告。

- 修复 Unity Beta 版本的分析版本。

- 修复命中断点或单步执行时变量不会显示在局部变量窗口中这一问题。

- 修复 Visual Studio 2013 中的变量工具提示。

- 修复 Unity 4.5 的 IntelliSense 文档生成。

- 修复重新加载域后的 Unity/Visual Studio 通信（Unity 中的播放/停止）。

- 修复对 Visual Studio 主题各部分的处理。

> [!IMPORTANT]
> C# 是 Unity 生态系统中的主要语言（即新的示例资产均以 C# 表示，Unity 文档将默认采用 C#），我们删除了对 UnityScript 和 Boo 的基本支持，以便更好地关注 C# 体验。 因此，VSTU 解决方案现在仅使用 C#，加载速度更快。

## <a name="1820"></a>1.8.2.0

发布时间：2014 年 1 月 7 日

### <a name="new-features"></a>新增功能

- 解决适用于编辑器远程发现的 Mavericks 上 Unity 脚本引擎网络层中的问题。

- 处理新端口，以发现远程 Unity 播放器。

- 引用特定于当前生成目标的 UnityEngine 程序集。

- 添加用于筛选要包括在所生成项目中的文件中的设置。

- 添加禁用向 Visual Studio 错误列表发送控制台日志的设置。 如果使用的是 PlayMaker 或 Console Pro，这将很有用，因为只能在 Unity 中注册一个回调，以接收控制台日志。

- 添加禁用 mdb 调试符号的生成的设置。 自己生成 mdb 时，这将很有用。

### <a name="bug-fixes"></a>Bug 修复

- 从 4.2 及以上版本的 Unity、在 VS 中打开的文件将丢失 IntelliSense 时修复回归。

- 修复 VS 对话框以处理自定义主题。

- 修复 UPE 的上下文菜单的关闭。

- 当版本特定生成的程序集不同步时，防止 Unity 中发生崩溃。

## <a name="1810"></a>1.8.1.0

发布时间：2013 年 11 月 21 日

### <a name="new-features"></a>新增功能

- 调整了 MonoBehaviour 向导与 Unity 4.3 API。

- MonoBehaviour 向导将根据你使用的版本筛选 Unity API。

- 为 Unity 4.1 以上版本的项目添加对 System.Xml.Linq 的引用。

- 整理对 Debug.Log 的调用，以便不在消息中包括 stacktrace 的开头。

### <a name="bug-fixes"></a>Bug 修复

- 修复了将影响 Visual Studio 中对 JavaScript 文件的默认处理的 bug。

- 此次实际修复了在 VS 中出现的白色像素这一问题。

- 修复了 UnityVS.VersionSpecific 程序集的删除问题（如果该程序集由 SCM 标记为只读）。

- 修复了在 UnityVS 包中创建套接字时出现的异常。

- 修复了从 Visual Studio 程序集中加载股票图像时 Visual Studio 中的崩溃问题。

- 修复了生成 Unity 源版本的 UnityVS.VersionSpecific 过程中的 bug。

- 修复了在 Unity 包中打开套接字时可能发生的冻结。

- 修复了对名称含短划线 (-) 的 Unity 项目的处理。

- 修复了从 Unity 打开脚本的问题，以便不混淆 Unity 4.2 及更高版本的 ALT+TAB 顺序。

## <a name="1800"></a>1.8.0.0

发布时间：2013 年 9 月 24 日

### <a name="new-features"></a>新增功能

- 极大地提高了调试器的连接速度。

- 自动处理到 Unity 4.2 及更高版本中的文件和行的导航。

- 条件断点。

- 项目文件生成器目前可处理 T4 模板。

- 使用新的 API 更新 MonBehavior 向导。

- C# 中适用于 Unity 类型的 IntelliSense 文档。

- 算术和逻辑表达式计算。

- 远程调试预览具有更好的远程编辑器发现能力。

### <a name="bug-fixes"></a>Bug 修复

- 修复了断开调试器连接后，可能在 VS 中泄露线程的 bug。

- 修复了在 VS 中出现的白色像素。

- 修复了对状态栏图标的点击的处理。

- 修复了使用“插件”文件夹中的程序集生成引用的问题。

- 修复了发生异常时从 UnityVS 包创建套接字的问题。

- 修复了对 UnityVS 新版本的检测。

- 修复了许可证过期时许可证管理器的提示问题。

- 修复了在 VS 进程窗口的附加调试器中呈现空进程列表的 bug。

- 修复了局部视图中不断变化的布尔值。

## <a name="1220"></a>1.2.2.0

发布时间：2013 年 7 月 9 日

### <a name="bug-fixes"></a>Bug 修复

- 处理表达式计算器中的完全限定名。

- 修复了与异常处理相关的冻结问题，其中 Unity 脚本引擎向我们发送不正确的堆栈帧数据。

- 修复了 Web 目标的生成过程。

- 修复了 Visual Studio 已启动并且已删除的文件位于要在启动时打开的文件列表中时可能发生的错误。

- 修复了 UnityVS.OpenFile，以处理非脚本文件，如编译的着色器。

- 现在从所有 C# 项目中引用 Boo.Lang 和 UnityScript.Lang。

- 修复了项目中引用的生成问题（假如项目具有特殊字符）。

- 解决对已释放项目的方法调用会触发多个 NullReferenceException MessageBox 的 VS 问题。

- 修复了 Unity 4.2 Beta 版程序集的处理问题。

## <a name="1210"></a>1.2.1.0

发布时间：2013 年 4 月 9 日

### <a name="bug-fixes"></a>Bug 修复

- 修复了发生 IO 错误时 Unity 程序集本地部署的代码完成错误（如只读文件，或由 Visual Studio 锁定的文件）。

- 修复了文件已在 Visual Studio 中打开时从 Unity 打开脚本将不会关注此文件的回归问题。

- 修复了新的异常处理的性能问题。

- 修复了某些外部 DLL 中断点绑定问题。

## <a name="1200"></a>1.2.0.0

发布时间：2013 年 3 月 25 日

### <a name="new-features"></a>新增功能

- 极大地提高了调试器的连接速度。

- 优化了针对大型项目的 Unity 项目资源管理器。

- 服从 Visual Studio 设置以中断（或不中断）已处理和未处理的异常。

- 服从 Visual Studio 设置，以调用局部变量上的 ToString。

- 添加新菜单“调试”>“附加 Unity 调试器”，可用于调试 Unity 播放器。

- 保留生成解决方案文件时添加到 UnityVS 解决方案中的自定义项目。

- 添加新的键盘快捷键 CTRL+ALT+M-> CTRL+H，以便在插入点位置处为 Unity 函数或成员显示 Unity 文档。

- 从 Visual Studio 进行编译时，将编译器响应文件 (rsp) 纳入考虑。

- 解构编译器生成的类型，以在调试生成器方法时显示变量。

- 通过消除配置 Unity 的共享文件夹的必要来简化远程调试。 现在只需具有从 Windows 访问 Unity 项目的权限。

- 将自定义 Unity 配置文件作为标准的 .net target 配置文件安装。 这修复了 ReSharper 可能显示的所有误报。

- 解决 Unity 脚本引擎 bug，以便调试器不会中断非正常注册的线程。

- 重新运行文件打开工具，以避免 VS 中的争用条件，此条件在文件打开请求崩溃时声明能够打开文件。

- UnityVS 现在请求在 VS 生成项目时（而不再是保存文件时）刷新生成。

### <a name="bug-fixes"></a>Bug 修复

- 修复了自定义的 .net 配置文件

- 修复了主题集成，即修复了 VS 2012 深色主题问题。

- 修复了 VS 2012 中的快速行为快捷方式。

- 修复了进行调试且非主线程将命中断点时可能发生的单步执行问题。

- 修复了类型别名的 UnityScript 和 Boo 完成，如 int。

- 修复了在编写新的 UnityScript 或 Boo 字符串时发生的异常。

- 修复了未加载解决方案时 Unity 菜单中的异常。

- 修复了 bug UV-48：键入双引号有时会产生错误并中断所有函数（代码完成、语法突出显示等）。

- 已修复 bug UVS-46：单击 Visual Studio 的“错误列表”时重复打开脚本文件 (UnityScript)。

- 已修复 bug UVS-42：状态栏中的 Unity 连接徽标不处理 VS 2012 中的鼠标事件。

- 已修复 bug UVS-44：VS 2012 中的 CTRL+SHIFT+Q 不可用于 Quick MonoBehaviours。

- 已修复 bug UV-40：VS2012“深色”主题中窗口为非活动状态时，Unity 项目资源管理器中的选定项目不可读。

- 已修复 bug UV-39：转义字符串标记化问题。

- 已修复 bug UV-35：检查相变量时调用对象上的 ToString。

- 已修复 bug UV-27：“转到符号”窗口与 VS2012 中的“深色”主题不一致。

- 已修复 bug UVS-11：协同例程中的局部变量。

## <a name="1100---beta-release"></a>1.1.0.0 - Beta 版本
发布时间：2013 年 3 月 9 日

## <a name="10130"></a>1.0.13.0
发布时间：2013 年 1 月 21 日

### <a name="bug-fixes"></a>Bug 修复

- 修复了目标调试对象发送无效的线程事件时可能发生的 Visual Studio 锁定问题。 在 OSX 上调试远程 Unity 时，通常会发生情况这样的问题。

- 修复了异常关闭调试器时可能出现的 Visual Studio 锁定问题。

- 修复了 C# MonoBehavior 位于命名空间中时的 MonoBehavior 帮助程序。

- 修复了 Visual Studio 2012 中 UnityScript 的调试器工具提示。

- 修复了仅从 Unity 更改调试常量时的项目生成。

- 修复了 Unity 项目资源管理器中的键盘导航。

- 修复了转义字符串的 UnityScript 着色。

- 修复了文件打开工具，以便在于 Unity 外部进行使用时更好地猜测项目名称。 用户在委托给 UnityVS 的 Unity 中使用第三方文件打开工具时，这是必需的。

- 修复了从 Unity 向 UnityVS 发送的长消息的处理。 在此之前，长消息可能会使 UnityVS 的消息传递部分崩溃。 因此，有时 UnityVS 不会从 Unity 打开文件。

## <a name="10120"></a>1.0.12.0
发布时间：2013 年 1 月 3 日

### <a name="bug-fixes"></a>Bug 修复

- 修复了 Visual Studio 删除断点时可能发生的 Visual Studio 锁定问题。

- 修复了 Unity 重新编译游戏脚本后不会命中某些断点的 bug。

- 修复了调试器，以在断点取消绑定时正确通知 Visual Studio。

- 修复了可能会阻止 Visual Studio 调试器调试本机程序的注册问题。

- 修复了计算 UnityScript 和 Boo 的表达式时可能发生的异常。

- 修复了一个回归，其中更改 Unity 中的 .NET API 级别不会触发项目文件更新。

- 修复了用户代码无法参与日志回调处理程序的 API 故障。

## <a name="10110"></a>1.0.11.0
发布时间：2012 年 11 月 28 日

### <a name="new-features"></a>新增功能

- Unity 4 的官方支持。

- 从 Unity 项目资源管理器操作脚本。

- Visual Studio 的“导航到”窗口中的集成。

- 分析信息控制台消息，使在错误列表中单击可将你带到第一个具有符号的堆栈帧。

- 添加 [API](../cross-platform/customize-project-files-created-by-vstu.md) 以使用户能够参与项目生成。

- 添加 [API](../cross-platform/share-the-unity-log-callback-with-vstu.md) 以使用户能够参与 LogCallback。

### <a name="bug-fixes"></a>Bug 修复

- 修复了 Visual Studio 2012 中 Unity 项目资源管理器后台的回归问题。

- 修复了完整 .net 配置文件的用户的项目生成。

- 修复了 Web 目标用户的项目生成。

- 修复了项目生成，以便像 Unity 那样，包括 DEBUG 和 TRACE 编译符号。

- 修复了在“转到符号”窗口中使用特殊字符时的崩溃。

- 修复了不能在 Visual Studio 状态栏中注入图标的崩溃。

## <a name="10100"></a>1.0.10.0
发布时间：2012 年 10 月 9 日

### <a name="bug-fixes"></a>Bug 修复

- 修复了 Visual Studio 2010 中 Unity 项目资源管理器的后台问题。

- 修复了 UnityVS 尝试将调试器附加到 Unity（其调试器界面先前已崩溃）时可能发生的 Visual Studio 冻结。

- 修复了设置断点且 AppDomain 会重新加载时可能发生的 Visual Studio 冻结。

- 修复了从 Unity 检索程序集的方式，以避免锁定文件和干扰 Unity 生成进程。

## <a name="1090"></a>1.0.9.0

发布时间：2012 年 10 月 3 日

### <a name="bug-fixes"></a>Bug 修复

- 修复了 Unity 项目包括实际 JavaScript 资产时的项目生成。

- 修复了表达式计算中的错误处理。

- 修复了将新值设置为值类型字段的问题。

- 修复了将光标悬停在代码编辑器中的表达式上时可能产生的副作用。

- 修复了在加载的程序集中为表达式计算搜索类型的方式。

- 已修复 bug UV-21：对 Unity 对象分配的评估不起作用。

- 已修复 bug UV-21：评估对 Unity Math API 的方法调用时的指针无效。

## <a name="1080"></a>1.0.8.0

发布时间：2012 年 9 月 26 日

### <a name="bug-fixes"></a>Bug 修复

- 修复了脚本打开工具获取项目路径的方式，以确保能够打开 Visual Studio 以及脚本。

- 修复了在调试会话运行时创建断点的 bug，此 bug 可能会导致 Visual Studio 锁定。

- 修复了在 Visual Studio 2010 中注册 UnityVS 的方式。

## <a name="1070"></a>1.0.7.0

发布时间：2012 年 9 月 14 日

### <a name="new-features"></a>新增功能

- Visual Studio 2012 支持。

### <a name="bug-fixes"></a>Bug 修复

- 修复了编辑器和插件项目文件的生成，以匹配 Unity 的行为。

- 修复了 Unity 4 中 .pdb 符号的转换。

> [!IMPORTANT]
> 由于 Visual Studio 2012 支持，我们不得不重命名几个文件并移动某些其他文件。 要导入 Unity 的 UnityVS 包现在分别为 Visual Studio 2010 和 Visual Studio 2012 命名为 UnityVS 2010 或 UnityVS 2012。 此版本还需要重新生成 UnityVS 项目文件。

## <a name="1060---internal-build"></a>1.0.6.0 - 内部版本
发布时间：2012 年 9 月 12 日

## <a name="1050"></a>1.0.5.0

发布时间：2012 年 9 月 10 日

### <a name="bug-fixes"></a>Bug 修复

- 修复了脚本或着色器具有无效 xml 字符时项目文件的生成。

- 修复了 Unity 连接到资产服务器时 Unity 实例的检测。 这会触发从 Unity 打开文件和自动连接 Visual Studio 调试器的失败。

## <a name="1040"></a>1.0.4.0

发布时间：2012 年 9 月 5 日

### <a name="new-features"></a>新增功能

- Unity 中调试符号的自动转换。

    如果资产文件夹中有 .NET .dll 程序集及其关联的 .pdb，只需重新导入程序集，UnityVS 就会将该 .pdb 转换为 Unity 的脚本引擎能够理解的调试符号文件，并且你能够从 UnityVS 单步执行自己的 .NET 程序集。

### <a name="bug-fixes"></a>Bug 修复

- 修复了由方法或 Unity 内部属性引发的异常导致调试时的 UnityVS 崩溃。

## <a name="1030"></a>1.0.3.0

发布时间：2012 年 9 月 4 日

### <a name="new-features"></a>新增功能

- 禁用使用 UnityVS 从 Unity 打开文件的新配置选项。

### <a name="bug-fixes"></a>Bug 修复

- 修复了对非编辑器项目的 UnityEditor 的引用的生成。

- 修复了非编辑器项目的 UNITY_EDITOR 符号的定义。

- 修复了由自定义状态栏导致的随机 VS 崩溃。

## <a name="1020"></a>1.0.2.0

发布时间：2012 年 8 月 30 日

### <a name="bug-fixes"></a>Bug 修复

- 修复了与 PythonTools 调试器的冲突。

- 修复了对 Mono.Cecil 的引用。

- 修复了使用 Unity 4 b7 从 Unity 检索脚本程序集的方式中的 bug。

## <a name="1010"></a>1.0.1.0

发布时间：2012 年 8 月 28 日

### <a name="new-features"></a>新增功能

- 对 Unity 4.0 Beta 的预览支持。

### <a name="bug-fixes"></a>Bug 修复

- 修复了对属性引发的异常的检查。

- 修复了检查对象时降序到基对象的问题。

- 修复了 MonoBehavior 向导中插入点的空白下拉列表。

- 修复了 UnityScript 和 Boo 的资产文件夹内 dll 的完成。

## <a name="1000---initial-release"></a>1.0.0.0 - 初始版本
发布时间：2012 年 8 月 22 日
