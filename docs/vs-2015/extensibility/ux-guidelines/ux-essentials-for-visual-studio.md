---
title: UX 基础知识
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: a793cf7a-f230-43ce-88d0-fa5d6f1aa9c7
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5f3ed2d3f8bc52b21f6a87ac7d6da00f665f6b28
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68181390"
---
# <a name="ux-essentials-for-visual-studio"></a>Visual Studio 的用户体验基础知识
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="best-practices"></a>最佳实践

### <a name="1-be-consistent-within-the-visual-studio-environment"></a>1.在 Visual Studio 环境中保持一致。

- 按照在 shell 中的现有交互模式。

- 设计功能与 shell 的 visual 语言和技能要求保持一致。

- 它们存在时，使用共享的命令和控件。

- 了解 Visual Studio 层次结构，以及如何建立上下文和驱动器 UI。

### <a name="2-use-the-environment-service-for-fonts-and-colors"></a>2.使用环境服务的字体和颜色。

- 除非公开自定义在选项对话框的字体和颜色页中，UI 应遵从的当前环境字体设置。

- UI 元素必须使用 VSColor Service，使用共享的环境令牌或特定于功能的令牌。

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
 Visual Studio Dev14 的最小分辨率为 1280 x 1024。 这意味着它是*可能*解析时，使用 Visual Studio，尽管这不是理想的用户体验。 则不能保证所有方面将都能使用分辨率低于 1280 x 1024。

 初始对话框大小不应超过 1000年像素的高度以适应此最小分辨率为 96 dpi IDE 的范围内。

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

 在这种情况下，没有其他问题由于用于警报的图标会包含"x"，因此常见的删除图标不能使用其旁边。 因此，UI 使用一个删除按钮，更笨拙的控件。

 ![清单设计器错误声明反&#45;模式](../../extensibility/ux-guidelines/media/manifestdesignererrordeclarationsanti-pattern.png "ManifestDesignererrordeclarationsanti 模式")

 **UI 置于错误状态默认情况下是 Visual Studio 反模式。**

#### <a name="alternatives"></a>替代项
 更好的解决方案，此问题是：

- 允许用户添加的声明而不发出警告，然后立即移动以在该项上设置属性。

- 添加警告图标 （金牌三角形） 时焦点将从移动项，如将另一个声明添加到列表，或尝试更改在设计器中的选项卡。

- 如果用户尝试设置属性上的任何声明之前更改选项卡，弹出一个对话框，说明该应用程序将无法生成 （或任何含义） 直到警告都得到解决。 如果用户关闭对话框并更改选项卡仍要然后图标 （严重或警告、 根据需要） 添加到声明选项卡。

### <a name="forcing-the-user-to-read-text-before-dismissing-ui"></a>强制用户关闭 UI 之前读取文本

#### <a name="feature-team-goals"></a>功能团队目标
 不允许用户关闭 UI，而无需首先查看说明文本。

#### <a name="anti-pattern"></a>后置反模式
 团队决定针对 X 的常见模式在 VS UI 中的各个位置插入视频的链接关闭按钮和工具提示说明指定的用户体验，并改为实现下拉列表中，"不要再显示"链接。

 ![解释性文本反&#45;模式&#45;不正确](../../extensibility/ux-guidelines/media/incorrectuseofmultipleclicks.png "Incorrectuseofmultipleclicks")

 **不正确： 强制用户之前需要阅读的解释性文本解除 UI 是 Visual Studio 中的反模式。**

#### <a name="result"></a>结果
 而不是简单的关闭按钮 （一次单击），强制用户使用两次单击只需关闭视频的链接将显示每个位置中的用户界面。

#### <a name="alternatives"></a>替代项
 这种情况下正确的设计是到 Internet Explorer、 Office 和 Visual Studio 遵循通用模式： 悬停时，用户可以看到工具提示说明，并单击一次隐藏 UI。

 ![解释性文本反&#45;模式&#45;正确](../../extensibility/ux-guidelines/media/explanatorytextanti-pattern-correct.png "Explanatorytextanti 模式更正")

 **正确： 按照设计，视频链接应显示的其他信息的工具提示，悬停时，并单击"X"应关闭消息无需进一步交互。**

### <a name="using-command-bars-for-settings"></a>使用命令栏设置
 ![命令栏反&#45;模式&#45;图](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurea.png "Commandbaranti 模式 FigureA")

 **图 a:命令栏反模式**

 **图 A**表示此反模式： 将下一个适用于多个只是命令的命令按钮的设置。 在这段代码中，有除了开始调试命令 — 等浏览器、 启动而无需调试和单步执行中的视图 — 将遵从了所选的设置。

 ![命令栏反&#45;模式&#45;图 B](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figureb.png "Commandbaranti 模式 FigureB")

 **图 b:更好，但仍命令栏反模式**

 如中所示稍好，但仍会将此类型的设置放在工具栏中，**图 B**。拆分按钮执行较少的空间，因此改进通过下拉列表，而这两个设计仍在使用工具栏以提升内容实际上并不是一个命令。

 ![命令栏反&#45;模式&#45;图 C](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurec.png "Commandbaranti 模式 FigureC")

 **图 c:Visual Studio 命令栏模式的正确使用**

 在中**图 C**，设置绑定到的一系列命令。 没有要设置没有全局设置，我们只需四个命令之间切换。 这是唯一一种在工具栏中的命令在可接受。

### <a name="control-anti-patterns"></a>控制反模式
 若干反模式是只是不正确的使用情况或表示法的控件或控件组。

#### <a name="underlining-used-as-a-group-label-not-a-hyperlink"></a>下划线作为组标签，而不是超链接
 下划线文本应仅用于超链接。

 **错误：**

 ![下划线反&#45;组标签中的模式](../../extensibility/ux-guidelines/media/0102-g-grouplabelincorrect.png "0102 g_GroupLabelIncorrect")

 **不是一个超链接的带下划线的文本是 Visual Studio 反模式。**

 **很好：**

 ![下划线反&#45;组标签中的模式&#40;正确&#41;](../../extensibility/ux-guidelines/media/0102-h-grouplabelcorrect.png "0102 h_GroupLabelCorrect")

 **正确设置的样式，非超链接文本显示未修饰环境字体中。**

#### <a name="clicking-on-a-check-box-results-in-a-pop-up-dialog"></a>单击弹出对话框中的复选框结果
 立即单击"发布 Windows Azure 应用程序"向导的"启用为所有角色的远程桌面"复选框将显示弹出对话框中，Visual Studio 反模式。 此外，复选框字段未填充有一个复选框后，选择另一种交互反模式。

 ![复选框 pop&#45;最反&#45;模式](../../extensibility/ux-guidelines/media/0102-i-checkboxpopup.png "0102 i_CheckboxPopup")

 **单击复选框，这是 Visual Studio 反模式后，将出现一个对话框。**

### <a name="hyperlink-anti-patterns"></a>超链接反模式
 下面的示例包含两个反模式。

1. 打开红色悬停时的前景色意味着未使用正确的共享的颜色从字体服务。

2. "了解详情"不是到概念主题的链接的相应文本。 用户的目标是不了解它是了解他们选择的后果。

   ![超链接反&#45;模式](../../extensibility/ux-guidelines/media/0102-j-hyperlinkincorrect.png "0102 j_HyperlinkIncorrect")

   **忽略颜色服务，并使用"了解更多"的超链接是 Visual Studio 反模式。**

   **更好的解决方案：** 会带来的问题，用户会询问单击的链接。

- Windows Azure 服务如何工作？

- 何时需要 Windows Azure 移动服务项目？

#### <a name="using-click-here-for-links"></a>使用"单击此处"链接
 超链接应该是自我描述。 它是一种反模式使用"单击此处"或任何类似的变体。

 **错误：** "单击此处了解有关如何创建一个新的项目。"

 **很好：** "如何创建一个新的项目？"
