---
title: 适用于 Unity 的 Visual Studio 工具概述 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-unity-tools
ms.topic: overview
ms.assetid: b4231bb9-45c4-4c77-ac3c-d05033b26393
caps.latest.revision: 6
ms.author: crdun
manager: crdun
ms.openlocfilehash: 27ef5a1f79b97a5be5583917f1c9703b3d624c16
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68183307"
---
# <a name="overview-of-visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity 的概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本部分将介绍更多有关 Visual Studio Tools for Unity 提供的功能的内容以及如何使用它们提高 Unity 的使用效率。  
  
 借助适用于 Unity 的 Visual Studio 工具 (VSTU  )，可以使用 Visual Studio 以 C# 编写游戏和编辑器脚本，随后使用其功能强大的调试器查找和修复错误。 VSTU 的最新版本包括用于 Unity 的 ShaderLab 着色器语言的语法着色、更好的调试器可视化效果以及针对 MonoBehavior 向导的改进的代码生成。 VSTU 还提供 Unity 项目文件、控制台消息以及在 Visual studio 中启动游戏的功能，从而使你可以在编写代码时花费更少的时间与 Unity 编辑器进行切换。  
  
 继续阅读以了解有关这些功能的详细信息。  
  
## <a name="integration-with-unity"></a>与 Unity 集成  
 如果不得不一直在 Unity 编辑器和 Visual Studio 之间来回切换，则 Visual Studio Tools for Unity 就不会是一个提升效率的工具。 这就是借助 Visual Studio Tools for Unity 可以轻松地在无需离开 Visual Studio 的情况下保持工作的原因。  
  
- “Unity 项目资源管理器”  使用在 Unity 编辑器中显示的相同层次结构在 Visual Studio 中显示整个 Unity 项目。  
  
- Unity 控制台集成将来自 Unity 控制台的输出显示在 Visual Studio 的错误窗口内的右侧。  
  
- 开始从 Visual Studio 调试你的游戏 – 无需切换回 Unity，只需按 F5。  
  
## <a name="superior-debugging"></a>出色的调试  
 将 Visual Studio 功能强大的调试器连接到你的 Unity 游戏以调试 C# 脚本和 Dll，无论它是在独立运行还是在 Unity 编辑器中运行。 可以使用你期望从 Visual Studio 获得的所有调试功能。  
  
- 断点，包括条件断点。  
  
- 计算“监视”窗口中的复杂表达式。  
  
- 检查和修改变量和参数的值。  
  
- 深化到复杂的对象和数据结构。  
  
  你甚至可以当 Unity 游戏在网络上的另一台计算机上运行时对其进行调试。  
  
## <a name="productivity"></a>工作效率  
 除了 Visual Studio 用于在 C# 中编写和重构代码的已有工作效率以外，Visual Studio Tools for Unity 为 Unity 开发人员提供了额外的工作效率功能。  
  
- Unity 的 ShaderLab 语言的语法着色可帮助你在着色器中的错误变成 bug 之前发现它们。 只需在 Visual Studio 中打开 ShaderLab 文件。  
  
- MonoBehavior 向导使你可以浏览 Unity 行为的列表并为你可能不熟悉的行为创建样板文件代码。 按 Ctrl+Shift+M。  
  
- 一旦你熟悉了最常使用的 Unity 行为，快速 MonoBehavior 向导会将其置于触手可及的地方。 按 Ctrl+Alt+Q。  
  
- 从 Visual Studio 访问 Unity 文档。 仅突出显示想要了解的 API 调用，然后按 Ctrl+Alt+M、Ctrl+H。  
  
- 使用键盘快捷方式访问所有这些功能以及更多功能。  
  
## <a name="visual-studio-tools-for-unity-api"></a>Visual Studio Tools for Unity API  
 使用提供的 API 自定义和扩展 Visual Studio Tools for Unity 的行为。  
  
- Visual Studio Tools for Unity 注册了一个日志回调，由此它可以将 Unity 控制台流式传输到 Visual Studio。 如果你有记录信息的编辑器脚本，可以将它们插入相同的回调以将消息发送给 Visual Studio。 有关详细信息，请参阅“日志回调”示例。  
  
- 可以通过使用 Unity 样式回调 ProjectFileGeneration 更改 Visual Studio Tools for Unity 生成项目文件的方式。 有关详细信息，请参阅项目文件生成示例。  
  
## <a name="see-also"></a>另请参阅  
 [Unity 主页](http://unity3d.com)
