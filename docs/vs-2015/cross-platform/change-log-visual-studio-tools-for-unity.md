---
title: 更改日志 (Visual Studio Tools for Unity) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: ea490b7e-fc0d-44b1-858a-a725ce20e396
caps.latest.revision: 14
author: conceptdev
ms.author: crdun
manager: jillfra
ms.openlocfilehash: 751faa1d81ca93fce5f8dfa866327cc8787e27ef
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825969"
---
# <a name="change-log-visual-studio-tools-for-unity"></a>更改日志（Visual Studio Tools for Unity）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio Tools for Unity 更改日志。

## <a name="23"></a>2.3

发布时间 2016-07-14

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

## <a name="22"></a>2.2

发布时间 2016-02-04

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

## <a name="21"></a>2.1

发布时间 2015-09-08

### <a name="new-features"></a>新增功能

- 支持 Unity 5.2

### <a name="bug-fixes"></a>Bug 修复

- 在低于 Unity 4.2 的版本中显示菜单项

- 当 Visual Studio 锁定 XML intellisense 文件时，不再显示错误消息。

- 当条件参数不是布尔值时处理 <\<When Changed>> 条件断点。

- 修复对 Windows 应用商店应用的 UnityEngine 和 UnityEditor 程序集的引用。

- 已修复在调试器中单步执行时的错误：无法单步执行，一般异常。

- 修复了 Visual Studio 2015 中的命中次数断点。

## <a name="20"></a>2.0

发布时间 2015-07-20

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

## <a name="20-preview-2"></a>2.0 预览版 2
发布日期 2015-04-02

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

- **UI：** Visual Studio 中已添加的 Visual Studio Tools for Unity“选项”对话框  。

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

## <a name="20-preview"></a>2.0 预览版
发布日期 2014-11-12

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

## <a name="192"></a>1.9.2

发布日期 2014-10-09

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

## <a name="191"></a>1.9.1

发布时间 2014-09-22

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

## <a name="19"></a>1.9

发布时间 2014-07-29

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

## <a name="182"></a>1.8.2

发布时间 2014-01-07

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

## <a name="181"></a>1.8.1

发布时间 2013-11-21

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

## <a name="180"></a>1.8.0

发布时间 2013-09-24

### <a name="new-features"></a>新增功能

- 极大地提高了调试器的连接速度。

- 自动处理到 Unity 4.2 及更高版本中的文件和行的导航。

- 条件断点。

- 项目文件生成器目前可处理 T4 模板。

- 使用新的 API 更新 MonBehavior 向导。

- C# 中适用于 Unity 类型的 Intellisense 文档。

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

## <a name="122"></a>1.2.2

发布时间 2013-07-09

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

## <a name="121"></a>1.2.1

发布时间 2013-04-09

### <a name="bug-fixes"></a>Bug 修复

- 修复了发生 IO 错误时 Unity 程序集本地部署的代码完成错误（如只读文件，或由 Visual Studio 锁定的文件）。

- 修复了文件已在 Visual Studio 中打开时从 Unity 打开脚本将不会关注此文件的回归问题。

- 修复了新的异常处理的性能问题。

- 修复了某些外部 DLL 中断点绑定问题。

## <a name="12"></a>1.2

发布时间 2013-03-25

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

## <a name="11--beta-release"></a>1.1 – Beta 版本
发布日期 2014-10-09

## <a name="1013"></a>1.0.13
发布日期 2013-01-21

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

## <a name="1012"></a>1.0.12
发布时间 2013-01-03

### <a name="bug-fixes"></a>Bug 修复

- 修复了 Visual Studio 删除断点时可能发生的 Visual Studio 锁定问题。

- 修复了 Unity 重新编译游戏脚本后不会命中某些断点的 bug。

- 修复了调试器，以在断点取消绑定时正确通知 Visual Studio。

- 修复了可能会阻止 Visual Studio 调试器调试本机程序的注册问题。

- 修复了计算 UnityScript 和 Boo 的表达式时可能发生的异常。

- 修复了一个回归，其中更改 Unity 中的 .NET API 级别不会触发项目文件更新。

- 修复了用户代码无法参与日志回调处理程序的 API 故障。

## <a name="1011"></a>1.0.11
发布时间 2012-11-28

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

## <a name="1010"></a>1.0.10
发布时间 2012-10-09

### <a name="bug-fixes"></a>Bug 修复

- 修复了 Visual Studio 2010 中 Unity 项目资源管理器的后台问题。

- 修复了 UnityVS 尝试将调试器附加到 Unity（其调试器界面先前已崩溃）时可能发生的 Visual Studio 冻结。

- 修复了设置断点且 AppDomain 会重新加载时可能发生的 Visual Studio 冻结。

- 修复了从 Unity 检索程序集的方式，以避免锁定文件和干扰 Unity 生成进程。

## <a name="109"></a>1.0.9

发布时间 2012-10-03

### <a name="bug-fixes"></a>Bug 修复

- 修复了 Unity 项目包括实际 JavaScript 资产时的项目生成。

- 修复了表达式计算中的错误处理。

- 修复了将新值设置为值类型字段的问题。

- 修复了将光标悬停在代码编辑器中的表达式上时可能产生的副作用。

- 修复了在加载的程序集中为表达式计算搜索类型的方式。

- 已修复 bug UV-21：对 Unity 对象分配的评估不起作用。

- 已修复 bug UV-21：评估对 Unity Math API 的方法调用时的指针无效。

## <a name="108"></a>1.0.8

发布时间 2012-09-26

### <a name="bug-fixes"></a>Bug 修复

- 修复了脚本打开工具获取项目路径的方式，以确保能够打开 Visual Studio 以及脚本。

- 修复了在调试会话运行时创建断点的 bug，此 bug 可能会导致 Visual Studio 锁定。

- 修复了在 Visual Studio 2010 中注册 UnityVS 的方式。

## <a name="107"></a>1.0.7

发布时间 2012-09-14

### <a name="new-features"></a>新增功能

- Visual Studio 2012 支持。

### <a name="bug-fixes"></a>Bug 修复

- 修复了编辑器和插件项目文件的生成，以匹配 Unity 的行为。

- 修复了 Unity 4 中 .pdb 符号的转换。

> [!IMPORTANT]
> 由于 Visual Studio 2012 支持，我们不得不重命名几个文件并移动某些其他文件。 要导入 Unity 的 UnityVS 包现在分别为 Visual Studio 2010 和 Visual Studio 2012 命名为 UnityVS 2010 或 UnityVS 2012。 此版本还需要重新生成 UnityVS 项目文件。

## <a name="106---internal-build"></a>1.0.6 - 内部版本
发布时间 2012-09-12

## <a name="105"></a>1.0.5

发布时间 2012-09-10

### <a name="bug-fixes"></a>Bug 修复

- 修复了脚本或着色器具有无效 xml 字符时项目文件的生成。

- 修复了 Unity 连接到资产服务器时 Unity 实例的检测。 这会触发从 Unity 打开文件和自动连接 Visual Studio 调试器的失败。

## <a name="104"></a>1.0.4

发布时间 2012-09-05

### <a name="new-features"></a>新增功能

- Unity 中调试符号的自动转换。

    如果资产文件夹中有 .NET .dll 程序集及其关联的 .pdb，只需重新导入程序集，UnityVS 就会将该 .pdb 转换为 Unity 的脚本引擎能够理解的调试符号文件，并且你能够从 UnityVS 单步执行自己的 .NET 程序集。

### <a name="bug-fixes"></a>Bug 修复

- 修复了由方法或 Unity 内部属性引发的异常导致调试时的 UnityVS 崩溃。

## <a name="103"></a>1.0.3

发布时间 2012-09-04

### <a name="new-features"></a>新增功能

- 禁用使用 UnityVS 从 Unity 打开文件的新配置选项。

### <a name="bug-fixes"></a>Bug 修复

- 修复了对非编辑器项目的 UnityEditor 的引用的生成。

- 修复了非编辑器项目的 UNITY_EDITOR 符号的定义。

- 修复了由自定义状态栏导致的随机 VS 崩溃。

## <a name="102"></a>1.0.2

发布时间 2012-08-30

### <a name="bug-fixes"></a>Bug 修复

- 修复了与 PythonTools 调试器的冲突。

- 修复了对 Mono.Cecil 的引用。

- 修复了使用 Unity 4 b7 从 Unity 检索脚本程序集的方式中的 bug。

## <a name="101"></a>1.0.1

发布时间 2012-08-28

### <a name="new-features"></a>新增功能

- 对 Unity 4.0 Beta 的预览支持。

### <a name="bug-fixes"></a>Bug 修复

- 修复了对属性引发的异常的检查。

- 修复了检查对象时降序到基对象的问题。

- 修复了 MonoBehavior 向导中插入点的空白下拉列表。

- 修复了 UnityScript 和 Boo 的资产文件夹内 dll 的完成。

## <a name="10--initial-release"></a>1.0 – 初始版本
发布时间 2012-08-22
