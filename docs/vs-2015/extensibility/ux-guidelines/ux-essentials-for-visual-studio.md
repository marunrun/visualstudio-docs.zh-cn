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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68181390"
---
# <a name="ux-essentials-for-visual-studio"></a>Visual Studio 用户体验基础知识
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="best-practices"></a>最佳实践

### <a name="1-be-consistent-within-the-visual-studio-environment"></a>1. 在 Visual Studio 环境中保持一致。

- 在 shell 内遵循现有交互模式。

- 设计功能与 shell 的视觉语言和追求要求保持一致。

- 使用共享命令和控件（如果存在）。

- 了解 Visual Studio 层次结构以及它如何建立上下文和驱动 UI。

### <a name="2-use-the-environment-service-for-fonts-and-colors"></a>2. 将环境服务用于字体和颜色。

- UI 应遵循当前环境字体设置，除非在 "选项" 对话框的 "字体和颜色" 页中对其进行自定义。

- UI 元素必须使用共享环境令牌或功能特定的令牌来使用 VSColor 服务。

### <a name="3-make-all-imagery-consistent-with-the-new-vs-style"></a>3. 使所有图像与新的 VS 样式一致。

- 按照 Visual Studio 设计原则，查看图标、字形和其他图形。

- 不要在图形元素中放置文本。

### <a name="4-design-from-a-user-centric-perspective"></a>4. 从以用户为中心的角度进行设计。

- 在任务流中的各个功能之前创建它。

- 熟悉你的用户，并在你的规范中明确了解这一知识。

- 查看 UI 时，请评估完整体验以及详细信息。

- 设计用户界面，使其保持正常运行，无需考虑区域设置或语言。

## <a name="screen-resolution"></a>屏幕分辨率

### <a name="minimum-resolution"></a>最小分辨率
 最小分辨率适用于 Visual Studio Dev14。 这 *意味着可以在* 此解决方案中使用 Visual Studio，但这可能不是最佳的用户体验。 不保证在分辨率低于1280x1024 的情况下，所有方面都能使用。

 初始对话框的高度不应超过1000像素，因此，在此最低分辨率下，可适应 IDE 帧 96 dpi。

### <a name="high-density-displays"></a>高密度显示
 Visual Studio 中的 UI 必须适用于 Windows 支持的所有 DPI 缩放系数：150%、200% 和250%。

## <a name="anti-patterns"></a>若干反模式
 Visual Studio 包含多个遵循指导原则和最佳做法的 UI 示例。 为了保持一致，开发人员通常会从类似于所构建内容的产品 UI 设计模式借用。 尽管这是一种可帮助我们在用户交互和可视化设计中推动一致性的好方法，但我们还是会提供一些详细信息，这些功能不符合我们的指导原则，因为计划限制或缺陷优先顺序。 在这些情况下，我们不希望团队复制这些 "反模式" 之一，因为它们会在 Visual Studio 环境中增加错误或不一致的 UI。

### <a name="required-fieldssettings-shown-in-error-state-by-default"></a>默认情况下，所需字段/设置显示为错误状态

#### <a name="feature-team-goals"></a>功能团队目标

- 警告用户他们添加了必须配置的元素。

- 将用户的注意力吸引到需要输入的区域。

#### <a name="anti-pattern-solution"></a>反模式解决方案
 用户启动了某个操作并在完成该任务之前，立即将关键停止图标置于需要配置的区域旁边。

#### <a name="example-manifest-designer-declarations"></a>示例：清单设计器声明
 向列表中添加声明后，会立即将其置于错误状态，这会一直保持，直到用户设置所需属性。

 在这种情况下，有一个额外的问题，因为用于警报的图标包含一个 "x"，因此不能在该图标旁边使用公用删除图标。 因此，UI 使用 "删除" 按钮，这是一个笨的控件。

 ![清单设计器错误声明反&#45;模式](../../extensibility/ux-guidelines/media/manifestdesignererrordeclarationsanti-pattern.png "ManifestDesignererrordeclarationsanti-模式")

 **默认情况下，将 UI 置于错误状态是 Visual Studio 的反模式。**

#### <a name="alternatives"></a>备选方法
 此问题的一个更好的解决方案是：

- 允许用户在不发出警告的情况下添加声明，然后立即移动以设置该项的属性。

- 当焦点从项移动时) 添加警告图标 (金色三角形，如将另一个声明添加到列表中或尝试更改设计器中的选项卡。

- 如果用户在设置任何声明的属性之前尝试更改选项卡，则会弹出一个对话框，说明该应用程序将不会生成 (或任何含义) 直到解决这些警告。 如果用户关闭对话框并更改选项卡，则在将相应的) 添加到 "声明" 选项卡时，将更改选项卡， (严重或警告。

### <a name="forcing-the-user-to-read-text-before-dismissing-ui"></a>强制用户在关闭用户界面之前读取文本

#### <a name="feature-team-goals"></a>功能团队目标
 不允许用户在没有首先看到说明文本的情况下关闭 UI。

#### <a name="anti-pattern"></a>反模式
 将视频链接插入到 VS UI 内的不同位置的团队根据 UX 指定的 X "关闭" 按钮和工具提示说明的常见模式决定，并改为实现下拉列表和 "不再显示" 链接。

 ![解释性文本反&#45;模式 &#45; 不正确](../../extensibility/ux-guidelines/media/incorrectuseofmultipleclicks.png "Incorrectuseofmultipleclicks")

 **错误：在关闭 UI 之前强制用户读取说明性文本在 Visual Studio 中为反模式。**

#### <a name="result"></a>结果
 用户只需单击一次鼠标) ，而不是简单的 "关闭" (按钮，用户只需单击两下鼠标，即可在视频链接显示的每个位置都关闭 UI。

#### <a name="alternatives"></a>备选方法
 对于这种情况，正确的设计是遵循 Internet Explorer、Office 和 Visual Studio 的通用模式：悬停时，用户可以看到工具提示说明，单击一次即可隐藏 UI。

 ![解释性文本反&#45;模式 &#45; 正确](../../extensibility/ux-guidelines/media/explanatorytextanti-pattern-correct.png "Explanatorytextanti-模式-正确")

 **正确：按照设计，视频链接应显示带有悬停相关附加信息的工具提示，单击 "X" 应关闭该消息，而无需进一步交互。**

### <a name="using-command-bars-for-settings"></a>使用命令栏进行设置
 ![命令栏反&#45;模式 &#45; 图 A](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurea.png "Commandbaranti-FigureA")

 **图 A：命令栏反模式**

 **图 A** 表示这种反模式：将设置置于仅适用于命令的命令按钮的下面。 在此草拟中，除了开始调试以外，还有一些命令，例如，在浏览器中进行查看、在不调试的情况下启动和单步执行，将遵循所选的设置。

 ![命令栏反&#45;模式 &#45; 图 B](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figureb.png "Commandbaranti-FigureB")

 **图 B：更好，但仍然是命令栏反模式**

 稍微好一点，但仍不希望将此类型的设置放在工具栏中，如 **图 B**所示。虽然拆分按钮需要较少的空间，因此，这种改进对下拉控制，但这两种设计仍使用工具栏来升级不是真正的命令的内容。

 ![命令栏反&#45;模式 &#45; 图 C](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurec.png "Commandbaranti-FigureC")

 **图 C：正确使用 Visual Studio 命令栏模式**

 在 **图 C**中，该设置绑定到一系列命令。 没有设置全局设置，我们只是在四个命令之间切换。 在这种情况下，工具栏中的命令是可接受的。

### <a name="control-anti-patterns"></a>控制反模式
 有些反模式只是错误地使用或表示控件或控件组。

#### <a name="underlining-used-as-a-group-label-not-a-hyperlink"></a>用作组标签而不是超链接的下划线
 下划线文本应仅用于超链接。

 **Dfx**

 ![标记组标签中的反&#45;模式](../../extensibility/ux-guidelines/media/0102-g-grouplabelincorrect.png "0102-g_GroupLabelIncorrect")

 **不是超链接的带下划线文本是 Visual Studio 反模式。**

 **良好**

 ![为组标签中的反&#45;模式加下划线 &#40;正确&#41;](../../extensibility/ux-guidelines/media/0102-h-grouplabelcorrect.png "0102-h_GroupLabelCorrect")

 **样式正确，非超链接文本在环境字体中显示未修饰。**

#### <a name="clicking-on-a-check-box-results-in-a-pop-up-dialog"></a>单击复选框会生成一个弹出式对话框。
 单击 "发布 Windows Azure 应用程序" 向导中的 "为所有角色启用远程桌面" 复选框会立即显示一个 Visual Studio 反模式的弹出对话框。 此外，选中复选框后，复选框字段不会填充复选框，另一种交互反模式。

 ![复选框弹出&#45;反&#45;模式](../../extensibility/ux-guidelines/media/0102-i-checkboxpopup.png "0102-i_CheckboxPopup")

 **单击复选框后显示一个对话框是 Visual Studio 的反模式。**

### <a name="hyperlink-anti-patterns"></a>超链接反模式
 下面的示例包含两个反模式。

1. 悬停时的前景红色表示不使用字体服务中的正确共享颜色。

2. "了解详细信息" 不是指向概念主题的链接的相应文本。 用户的目标不是了解详细信息，而是了解他们选择的后果。

   ![Hyperlink 反&#45;模式](../../extensibility/ux-guidelines/media/0102-j-hyperlinkincorrect.png "0102-j_HyperlinkIncorrect")

   **忽略颜色服务，并使用 "了解更多" 超链接为 Visual Studio 反模式。**

   **更好的解决方案：** 单击链接，提出用户要询问的问题。

- Windows Azure 服务的工作原理是什么？

- 何时需要 Windows Azure 移动服务项目？

#### <a name="using-click-here-for-links"></a>为链接使用 "单击此处"
 超链接应是自描述性的。 这是一种可使用 "单击此处" 或任何类似变体的反模式。

 **错误：** 单击此处了解有关如何创建新项目的说明。

 **不错：** "如何实现创建新项目？"
