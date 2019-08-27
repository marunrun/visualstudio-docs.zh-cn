---
title: Visual Studio 的用户体验基础知识 |Microsoft Docs
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: a793cf7a-f230-43ce-88d0-fa5d6f1aa9c7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 45e4f1389317c67665d1b03e936a33380cb7ecf2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310812"
---
# <a name="ux-essentials-for-visual-studio"></a>Visual Studio 的用户体验基础知识

## <a name="best-practices"></a>最佳实践

### <a name="1-be-consistent-within-the-visual-studio-environment"></a>1.在 Visual Studio 环境中保持一致。

- 请按照现有[交互模式](interaction-patterns-for-visual-studio.md)在 shell 中。

- 设计功能，使其与 shell 的 visual 语言一致并[耕耘要求](evaluation-tools-for-visual-studio.md)。

- 它们存在时，使用共享的命令和控件。

- 了解 Visual Studio 层次结构，以及如何建立上下文和驱动器 UI。

### <a name="2-use-the-environment-service-for-fonts-and-colors"></a>2.使用环境服务的字体和颜色。

- UI 应遵循当前[环境字体](fonts-and-formatting-for-visual-studio.md)设置，除非在选项对话框的字体和颜色页中的自定义公开。

- UI 元素必须使用[VSColor Service](colors-and-styling-for-visual-studio.md)，使用共享环境令牌或特定于功能的令牌。

### <a name="3-make-all-imagery-consistent-with-the-new-vs-style"></a>3.使所有图像与新的 VS 样式一致。

- 请按照 Visual Studio 的图标、 字形和其他图形的设计原则。

- 不要将文本放在图形元素。

### <a name="4-design-from-a-user-centric-perspective"></a>4.设计从以用户为中心的角度来看。

- 创建任务流之前在其中的各个功能。

- 熟悉你的用户和你规范中明确这一知识。

- 在检查时用户界面，评估完整的体验，以及详细信息。

- 设计你的 UI，以便它仍然适用且吸引人，而不考虑区域设置或语言。

## <a name="screen-resolution"></a>屏幕分辨率

### <a name="minimum-resolution"></a>最小分辨率

- Visual Studio 2015 的最小分辨率**1280 x 720**。 这意味着它是*可能*解析时，使用 Visual Studio，尽管这不是理想的用户体验。 没有保证所有方面都为分辨率低于 1280 x 720 可用。

- Visual Studio 的目标解决方法是**1366 x 768**。 这是在其中我们承诺的最低分辨率*好*用户体验。

- 初始对话框的高度应**小于 700 像素**，因此它适合在 96 dpi，在 IDE 框架的最小分辨率。

### <a name="high-density-displays"></a>高密度显示
 Visual Studio 中的 UI 必须适用于 Windows 支持在初始状态下的所有 DPI 缩放因素：150%、 200%和 250%。

## <a name="anti-patterns"></a>反模式
 Visual Studio 包含许多 UI 的示例，请按照我们的指导原则和最佳实践。 为了保持一致，开发人员通常借用产品 UI 设计模式类似于他们在开发。 尽管这是一个不错的方法，可帮助我们驱动器的用户交互和直观设计保持一致，我们有时提供功能的一些详细信息不满足我们的指导原则由于计划限制或脱离优先顺序。 在这些情况下，我们不希望复制其中一种"反模式"的团队因为它们数量不正确或不一致的 UI，在 Visual Studio 环境的不断增加。

### <a name="required-fieldssettings-shown-in-error-state-by-default"></a>默认情况下显示处于错误状态所需的字段/设置

#### <a name="feature-team-goals"></a>功能团队目标

- 警告用户他们已添加了必须配置的元素。

- 提醒用户注意需要输入的区域。

#### <a name="anti-pattern-solution"></a>后置反模式解决方案
 只要用户启动的操作，它们已完成任务之前，立即将关键停止图标旁边需要配置的区域。

#### <a name="example-manifest-designer-declarations"></a>示例:清单设计器声明
 立即向列表添加一个声明将将其放在错误状态，仍然存在，直到用户设置所需的属性。

 在这种情况下，没有其他需考虑因为用于警报的图标会包含"&times;"图标，因此常见的删除图标不能使用其旁边。 因此，UI 使用一个删除按钮，更笨拙的控件。

 ![UI 置于错误状态默认情况下是 Visual Studio 反模式。](../../extensibility/ux-guidelines/media/manifestdesignererrordeclarationsanti-pattern.png "ManifestDesignererrordeclarationsanti 模式")<br />UI 置于错误状态默认情况下是 Visual Studio 反模式。

#### <a name="alternatives"></a>替代项

更好的解决此问题是：

- 允许用户添加的声明而不发出警告，然后立即移动以在该项上设置属性。

- 添加警告图标 （金牌三角形） 时焦点将从移动项，如将另一个声明添加到列表，或尝试更改在设计器中的选项卡。

- 如果用户尝试设置属性上的任何声明之前更改选项卡，弹出一个对话框，说明该应用程序将无法生成 （或任何含义） 直到警告都得到解决。 如果用户关闭对话框并更改选项卡仍要然后图标 （严重或警告、 根据需要） 添加到声明选项卡。

### <a name="multiple-clicks-to-dismiss-ui"></a>多个单击操作即可关闭用户界面

#### <a name="feature-team-goals"></a>功能团队目标
 不允许用户关闭 UI，而无需首先查看说明文本。

#### <a name="anti-pattern"></a>后置反模式
 针对常见的模式，插入到 VS UI 中的各个位置的视频链接该团队决定"&times;"与的关闭按钮和工具提示说明指定的用户体验，并改为实现一个下拉列表和"不要再显示"链接。

#### <a name="example-video-links-in-team-explorer"></a>示例:在团队资源管理器中的视频链接
强制用户之前需要阅读的解释性文本解除 UI 是 Visual Studio 中的反模式。 正确设计的视频链接应显示的其他信息的工具提示上悬停时，并单击"&times;"应关闭消息无需进一步交互。

 ![解释性文本反&#45;模式&#45;不正确](../../extensibility/ux-guidelines/media/incorrectuseofmultipleclicks.png "Incorrectuseofmultipleclicks")<br />视频链接不正确的模式

而不是简单的关闭按钮 （一次单击），强制用户使用两次单击只需关闭视频的链接将显示每个位置中的用户界面。

这种情况下正确的设计是到 Internet Explorer、 Office 和 Visual Studio 遵循通用模式： 悬停时，用户可以看到工具提示说明，并单击一次隐藏 UI。

 ![解释性文本反&#45;模式&#45;正确](../../extensibility/ux-guidelines/media/explanatorytextanti-pattern-correct.png "Explanatorytextanti 模式更正")<br />正确的视频链接模式

### <a name="using-command-bars-for-settings"></a>使用命令栏设置

**图 A**表示此反模式： 将下一个适用于多个只是命令的命令按钮的设置。 在这段代码中，有除了开始调试命令 — 等浏览器、 启动而无需调试和单步执行中的视图 — 将遵从了所选的设置。

![图 a:命令栏反模式](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurea.png "Commandbaranti 模式 FigureA")<br />图 a:命令栏反模式

如中所示稍好，但仍会将此类型的设置放在工具栏中，**图 B**。拆分按钮执行较少的空间，因此改进通过下拉列表，而这两个设计仍在使用工具栏以提升内容实际上并不是一个命令。

![图 b:更好，但仍命令栏反模式](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figureb.png "Commandbaranti 模式 FigureB")<br />图 b:更好，但仍命令栏反模式

在正确的方法中所示**图 C**，设置绑定到的一系列命令。 没有要设置没有全局设置，我们只需四个命令之间切换。 这是唯一一种在工具栏中的命令在可接受。

![图 c:Visual Studio 命令栏模式的正确用法](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurec.png "Commandbaranti 模式 FigureC")<br />图 c:Visual Studio 命令栏模式的正确使用

### <a name="control-anti-patterns"></a>控制反模式
 若干反模式是只是不正确的使用情况或表示法的控件或控件组。

#### <a name="underlining-used-as-a-group-label-not-a-hyperlink"></a>下划线作为组标签，而不是超链接
 下划线文本应仅用于超链接。

 **错误：** \
 ![不是一个超链接的带下划线的文本是 Visual Studio 反模式。](../../extensibility/ux-guidelines/media/0102-g_grouplabelincorrect.png "0102 g_GroupLabelIncorrect")<br />不是一个超链接的带下划线的文本是 Visual Studio 反模式。

 **很好：** \
 ![正确设置的样式，非超链接文本显示未修饰环境字体中。](../../extensibility/ux-guidelines/media/0102-h_grouplabelcorrect.png "0102 h_GroupLabelCorrect")<br />正确设置的样式，非超链接文本显示未修饰环境字体中。

#### <a name="clicking-on-a-check-box-results-in-a-pop-up-dialog"></a>单击弹出对话框中的复选框结果
 立即单击"发布 Windows Azure 应用程序"向导的"启用为所有角色的远程桌面"复选框将显示弹出对话框中，Visual Studio 反模式。 此外，复选框字段未填充有一个复选框后，选择另一种交互反模式。

 ![单击复选框，这是 Visual Studio 反模式后，将出现一个对话框。](../../extensibility/ux-guidelines/media/0102-i_checkboxpopup.png "0102 i_CheckboxPopup")<br />单击复选框，这是 Visual Studio 反模式后，将出现一个对话框。

### <a name="hyperlink-anti-patterns"></a>超链接反模式
 下面的示例包含两个反模式：

1. 打开红色悬停时的前景色意味着未使用正确的共享的颜色从字体服务。

2. "了解详情"不是到概念主题的链接的相应文本。 用户的目标是不了解它是了解他们选择的后果。

   ![忽略颜色服务，并使用"了解更多"的超链接是 Visual Studio 反模式。](../../extensibility/ux-guidelines/media/0102-j_hyperlinkincorrect.png "0102 j_HyperlinkIncorrect")<br />忽略颜色服务，并使用"了解更多"的超链接是 Visual Studio 反模式。

**更好的解决方案：** 会带来的问题，用户会询问单击的链接。 例如：

- Windows Azure 服务如何工作？

- 何时需要 Windows Azure 移动服务项目？

#### <a name="using-click-here-for-links"></a>使用"单击此处"链接
 超链接应该是自我描述。 它是一种反模式使用"单击此处"或任何类似的变体。

 **错误：** "单击此处了解有关如何创建一个新的项目。"

 **很好：** "如何创建一个新的项目？"
