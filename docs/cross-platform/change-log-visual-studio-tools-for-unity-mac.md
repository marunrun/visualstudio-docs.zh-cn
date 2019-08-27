---
title: 更改日志（Visual Studio Tools for Unity、Mac）| Microsoft Docs
ms.custom: ''
ms.date: 04/02/2019
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: 33a6ac54-d997-4308-b5a0-af7387460849
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: ff2bcce9e041ff28393020c48563fe345c4fa076
ms.sourcegitcommit: 044bb54cb4552c8f4651feb11d62e52726117e75
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661822"
---
# <a name="change-log-visual-studio-tools-for-unity-mac"></a>更改日志（Visual Studio Tools for Unity、Mac）

Visual Studio Tools for Unity 更改日志。

## <a name="2200"></a>2.2.0.0

发布时间：2019 年 7 月 25 日

### <a name="bug-fixes"></a>Bug 修复

- **评估版：**

  - 修复了 IntPtr 类型的检测。

- **调试器：**

  - 修复了捕获点和函数断点的处理。

## <a name="2130"></a>2.1.3.0

发布时间：2019 年 7 月 9 日

### <a name="new-features"></a>新增功能

- **调试器：**

  - 增加了对捕获异常子类的支持。

  - 增加了对 MDS 协议 2.51 的支持。

- **集成：**

  - 增加了对 asmdef 文件的支持。

  - 从模板添加文件时切换到重命名模式（模仿 Unity 编辑器的行为）。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了与 Unity 播放器通信时格式错误消息的处理。

- **评估版：**

  - 修复了表达式中命名空间的处理。

## <a name="2120"></a>2.1.2.0

发布时间：2019 年 7 月 2 日

### <a name="bug-fixes"></a>Bug 修复

- **评估版：**

  - 修复了包含不可解析表达式的错误报告。

## <a name="2110"></a>2.1.1.0

发布时间：2019 年 6 月 27 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 已将 MonoBehaviour API 更新到 2019.1。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了 Unity 项目资源管理器的性能。

  - 启用轻型生成时，修复了要输出的报告警告和错误。

  - 修复了轻型生成性能。

## <a name="2100"></a>2.1.0.0

发布时间：2019 年 6 月 20 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 禁用了 Unity 项目的完整生成，取而代之的是使用 IntelliSense 错误和警告。 事实上，Unity 使用表示 Unity 内部所执行操作的类库项目创建 Visual Studio 解决方案。 尽管如此，Visual Studio 中的生成结果从未由 Unity 使用或选取，因为其编译管道已关闭。 在 Visual Studio 中生成只是使用资源。 如果由于你具有工具或具有依赖于完整生成的安装程序而需要完整生成，则可以禁用此优化（设置/Tools for Unity/禁用项目的完整生成）。
  
  - 添加了对 UPE 中的 Unity 包的支持。 只有引用包（使用 Packages 文件夹中的 manifest.json）和本地包（嵌入在 Packages 文件夹中）是可见的。

## <a name="2021"></a>2.0.2.1

发布时间：2019 年 5 月 30 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 增加了 Unity 执行目标的自定义图标。

## <a name="2020"></a>2.0.2.0

发布时间：2019 年 4 月 2 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对保存时自动刷新 Unity 资产数据库的支持。 这在默认情况下处于启用状态，当在 Visual Studio 中保存脚本时，将在 Unity 端触发重新编译。 保存时可以在“工具\选项\适用于 Unity 的工具\刷新 Unity 的 AssetDatabase”中禁用此功能。

  - 添加了对脱机文档设置首选 unity 安装的支持。

  - 添加了适用于新编辑器的上下文菜单。

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了空帧的程序集筛选和帧检查。

## <a name="2011"></a>2.0.1.1
 
 发布日期：2019 年 3 月 26 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 暂时将 Mono 设置为此特定版本的默认且唯一可用的调试器。

## <a name="2006"></a>2.0.0.6

发布日期：2019 年 3 月 26 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对“附加到 Unity 并播放”的支持。

## <a name="2005"></a>2.0.0.5

发布日期：2019 年 3 月 20 日

### <a name="new-features"></a>新增功能

- **项目生成：**

  - 处理解决方案文件时，请保留外部属性。

## <a name="2004"></a>2.0.0.4

发布日期：2019 年 3 月 5 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 更新了 ScriptableObject API。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 从模板中删除了命名空间。

## <a name="2003"></a>2.0.0.3
 
 发布日期：2019 年 3 月 5 日

### <a name="new-features"></a>新增功能

- **项目生成：**

  - 公共字段和序列化字段将不再引发警告。 在创建这些消息的 Unity 项目中，我们自动禁止了 CS0649 和 IDE0051 编译器警告。

- **集成：**

  - 如果运行多个 Unity 进程，系统将提示附加到特定实例。

- **评估版：**

  - 增加了对本地函数的支持。

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了在使用旧协议版本时读取命名参数的自定义属性。

## <a name="2002"></a>2.0.0.2

发布时间：2019 年 2 月 4 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 更新了 MonoBehaviour API。

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了在调试器中设置基元值。

## <a name="2001"></a>2.0.0.1

发布时间：2018 年 12 月 4 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了安装包的自包含。

## <a name="2000"></a>2.0.0.0
 发布时间：2018 年 12 月 4 日

### <a name="new-features"></a>新增功能

- **调试器：**

  - 用 Windows 上的同核心 Unity 调试程序替换了 Mac 上的 Unity 调试程序。

  - 将 NRefactory 替换为 Roslyn 以进行表达式计算。

  - 添加了对指针的支持：取消引用、强制转换和指针算法（为此同时需要 Unity 2018.2+ 和新运行时）。

  - 添加了对数组指针视图（例如在 C++ 中）的支持。 需要一个指针表达式，然后追加一个逗号和要查看的元素数。

  - 添加了对异步构造的支持。

  - 增加了对伪变量（异常和对象标识符）的支持。

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了表达式格式不正确或不受支持的表达式计算。

## <a name="1700"></a>1.7.0.0

发布时间：2018 年 11 月 13 日

### <a name="new-features"></a>新增功能

- **调试器：**

  - 在“附加”对话框中添加了更多客户端信息（IP、计算机名称）。

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了用于与 Unity 调试器引擎进行通信的库中的死锁，此死锁会导致 Visual Studio 或 Unity 冻结，尤其是在用户点击“附加到 Unity”或重启游戏时。

- **集成：**

  - 修复了选中另一个默认编辑器时 Unity 插件的激活。

  - 修复了 Unity 文件模板创建。

## <a name="1602"></a>1.6.0.2

发布时间：2018 年 7 月 24 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 回滚了针对 Unity 性能缺陷的解决方案（此缺陷已由 Unity 修复）。

## <a name="1601"></a>1.6.0.1

发布时间：2018 年 7 月 10 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 支持固定着色器代码着色。

## <a name="1600"></a>1.6.0.0

发布时间：2018 年 6 月 26 日

### <a name="bug-fixes"></a>Bug 修复

- **向导：**

  - 修复了 OnApplicationFocus 消息拼写错误。

- **项目生成：**

  - Unity 性能 Bug 的暂时解决方法：生成项目时缓存 MonoIsland。

  - 使用新版 Unity 运行时，不要再将可移植 pdb 转换为 mdb。

## <a name="1502"></a>1.5.0.2

发布时间：2018 年 4 月 18 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对基本着色器代码补全的支持。

  - 添加了对在着色器文件中切换注释的支持。

## <a name="1501"></a>1.5.0.1

发布时间：2018 年 3 月 28 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对 Unity 项目资源管理器中的额外模板的支持。

## <a name="1500"></a>1.5.0.0

发布时间：2018 年 3 月 21 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对检测并附加到通过 USB 连接的 Android 播放器的支持。

## <a name="1403"></a>1.4.0.3

发布时间：2018 年 3 月 5 日

### <a name="new-features"></a>新增功能

- **项目生成：**

  - 添加了对 Unity 2018.1 中新项目生成器的支持。

- **集成：**

  - 为专用设置添加了选项面板。

## <a name="1402"></a>1.4.0.2

发布时间：2018 年 1 月 24 日

### <a name="bug-fixes"></a>Bug 修复

- **项目生成：**

  - 修复了 Mono 版本检测的问题。

- **集成：**

  - 修复了 2018.1 和插件激活的计时问题。

  - 修复了检测新播放器时的通知。

## <a name="1401"></a>1.4.0.1

发布时间：2018 年 1 月 23 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了双击展开/折叠文件夹

## <a name="1400"></a>1.4.0.0

发布时间：2017 年 12 月 13 日

### <a name="new-features"></a>新增功能

- **项目生成：**

  - 添加了对 .NET Standard 的支持。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 固定自动 pdb 到 mdb 调试符号转换。

## <a name="1301"></a>1.3.0.1

发布时间：2017 年 12 月 12 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了在尝试更改数组大小时对 EditorPrefs.GetBool 的间接调用影响检查器的问题。

- **向导：**

  - 在插入方法前刷新 roslyn 上下文。

## <a name="1300"></a>1.3.0.0

发布时间：2017 年 11 月 20 日

### <a name="new-features"></a>新增功能

- **向导：**

  - 添加了“实现 Unity 消息”向导。

  - 添加了对 Mac 7.4 的 VS 中 API 新完成的支持。

## <a name="1200"></a>1.2.0.0

发布时间：2017 年 10 月 23 日

### <a name="new-features"></a>新增功能

- **调试器：**

  - 增加了对可移植调试符号文件的支持。

### <a name="bug-fixes"></a>Bug 修复

- **项目生成：**

  - 修复了额外 .dll 扩展名错误添加到程序集文件问题。

  - 不强制 AllowAttachedDebuggingOfEditor Unity，因为现在默认为“true”。

## <a name="1103"></a>1.1.0.3

发布时间：2017 年 10 月 23 日

### <a name="new-features"></a>新增功能

- **项目生成：**

  - 添加了对 .NET 4.6 配置文件的支持。

## <a name="1102"></a>1.1.0.2

发布时间：2017 年 8 月 8 日

### <a name="new-features"></a>新增功能

- **调试器：**

  - 如果不确定附加到哪个 Unity，启动“附加到进程”对话框。

- **项目生成：**

  - 使用 Unity 5.6 时，始终启用不安全编译开关。

## <a name="1101"></a>1.1.0.1

发布时间：2017 年 7 月 20 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对本地化资源的支持。

## <a name="1100"></a>1.1.0.0

发布时间：2017 年 7 月 12 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对通过“附加到进程”窗口附加到播放器和编辑器的支持。

- **项目生成：**

  - 修复了使用 mcs.rsp 文件的程序集名称引用。

  - 添加了对 assembly.json 编译单元的支持。

  - 修复了通过 API 级别进行定义的问题。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了编译时的着色器错误消息。

## <a name="1001"></a>1.0.0.1

发布时间：2017 年 5 月 4 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了混合和常规项目的活动文档跟踪。

## <a name="1000"></a>1.0.0.0

发布时间：2017 年 5 月 3 日
