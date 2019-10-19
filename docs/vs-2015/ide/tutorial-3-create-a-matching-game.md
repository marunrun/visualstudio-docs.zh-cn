---
title: 教程 3：创建匹配游戏 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 525815c8-2845-45e8-be96-100d1f144725
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1d67e81aa90faa59cf5320293aba9e7d82e3f625
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654730"
---
# <a name="tutorial-3-create-a-matching-game"></a>教程3：创建匹配游戏
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本教程中，将生成一个匹配游戏，在该游戏中，玩家必须匹配隐藏的图标对。 您将学习如何：

- 在 `List` 对象中存储对象，例如图标。

- 使用 `foreach` 循环（Visual C# 中）或 `For Each` 循环（Visual Basic 中）循环访问列表中的各项。

- 使用引用变量跟踪窗体的状态。

- 生成事件处理程序，以响应可用于多个对象的事件。

- 创建一个计时器，进行倒计时，然后在启动后立即准确触发事件。

  当你完成本教程时，程序将类似下图所示。

  ![本教程中创建的游戏](../ide/media/express-finishedgame.png "Express_FinishedGame")本教程中创建的游戏

  若要下载示例的完整版本，请参阅 [Complete Matching Game tutorial sample](http://code.msdn.microsoft.com/Complete-Matching-Game-4cffddba)（完整匹配游戏教程示例）。

> [!NOTE]
> 在本教程中，同时涉及 Visual C# 和 Visual Basic，因此请关注特定于您使用的编程语言的信息。

 如果你遇到困难或在编程方面有疑问，请尝试在一个 MSDN 论坛上发布你的问题。 请参阅 [Visual Basic 论坛](http://social.msdn.microsoft.com/Forums/home?forum=vbgeneral)和 [Visual C# 论坛](http://social.msdn.microsoft.com/Forums/home?forum=csharpgeneral)。 另外，那里有很好的免费视频学习资源供你使用。 若要了解有关 Visual Basic 编程的详细信息，请参阅 [Visual Basic Fundamentals: Development for Absolute Beginners](http://channel9.msdn.com/Series/Visual-Basic-Development-for-Absolute-Beginners)（Visual Basic 基础知识：零基础开发）。 若要了解有关 Visual C# 编程的详细信息，请参阅 [C# Fundamentals: Development for Absolute Beginners](http://channel9.msdn.com/Series/C-Sharp-Fundamentals-Development-for-Absolute-Beginners)（C# 基础知识：零基础开发）。

## <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[步骤 1：创建项目并向窗体添加表](../ide/step-1-create-a-project-and-add-a-table-to-your-form.md)|首先创建项目并添加 `TableLayoutPanel` 控件，以保持控件正确对齐。|
|[步骤 2：添加随机对象和图标列表](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)|添加 `Random` 对象和 `List` 对象，以创建图标列表。|
|[步骤 3：向每个标签分配一个随机图标](../ide/step-3-assign-a-random-icon-to-each-label.md)|将图标随机分配给 `Label` 控件，使每个游戏均不同。|
|[步骤 4：向每个标签添加一个 Click 事件处理程序](../ide/step-4-add-a-click-event-handler-to-each-label.md)|添加一个 Click 事件处理程序，该处理程序更改被单击的标签的颜色。|
|[步骤 5：添加标签引用](../ide/step-5-add-label-references.md)|添加引用变量以跟踪哪些标签被单击。|
|[步骤 6：添加计时器](../ide/step-6-add-a-timer.md)|向窗体中添加计时器，以记录游戏中逝去的时间。|
|[步骤 7：保持对可见](../ide/step-7-keep-pairs-visible.md)|保持图标对可见（如果选择了匹配的对）。|
|[步骤 8：添加方法以验证玩家是否获胜](../ide/step-8-add-a-method-to-verify-whether-the-player-won.md)|添加 `CheckForWinner()` 方法以验证玩家是否获胜。|
|[步骤 9：尝试其他功能](../ide/step-9-try-other-features.md)|尝试其他功能，例如更改图标和颜色、添加网格以及添加声音。 尝试使图板变大并调整计时器。|
