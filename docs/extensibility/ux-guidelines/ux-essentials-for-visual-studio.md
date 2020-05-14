---
title: 视觉工作室的 UX 要点 |微软文档
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: a793cf7a-f230-43ce-88d0-fa5d6f1aa9c7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c6c329eda477d77ab73be2ad913ac18d67ff3c08
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698329"
---
# <a name="ux-essentials-for-visual-studio"></a>Visual Studio 用户体验基础知识

## <a name="best-practices"></a>最佳做法

### <a name="1-be-consistent-within-the-visual-studio-environment"></a>1. 在视觉工作室环境中保持一致。

- 遵循 shell 中现有的[交互模式](interaction-patterns-for-visual-studio.md)。

- 设计特点与外壳的视觉语言和[工艺要求](evaluation-tools-for-visual-studio.md)一致。

- 当共享命令和控件存在时，请使用它们。

- 了解 Visual Studio 层次结构及其如何建立上下文并推动 UI。

### <a name="2-use-the-environment-service-for-fonts-and-colors"></a>2. 对字体和颜色使用环境服务。

- UI 应尊重当前[环境字体](fonts-and-formatting-for-visual-studio.md)设置，除非在"选项"对话框中的"字体和颜色"页中公开该设置以进行自定义。

- UI 元素必须使用[VSColor 服务](colors-and-styling-for-visual-studio.md)，使用共享环境令牌或特定于功能的令牌。

### <a name="3-make-all-imagery-consistent-with-the-new-vs-style"></a>3. 使所有影像与新 VS 样式保持一致。

- 遵循图标、字形和其他图形的可视化工作室设计原则。

- 不要将文本放在图形元素中。

### <a name="4-design-from-a-user-centric-perspective"></a>4. 从以用户为中心的角度进行设计。

- 在任务流之前创建任务流。

- 熟悉您的用户，并在您的规范中明确了解这些知识。

- 查看 UI 时，请评估完整的体验以及详细信息。

- 设计 UI，使其无论区域设置或语言如何，都能保持功能性和吸引力。

## <a name="screen-resolution"></a>屏幕分辨率

### <a name="minimum-resolution"></a>最小分辨率

- Visual Studio 2015 的最低分辨率为**1280x720**。 这意味着可以在此分辨率下*possible*使用 Visual Studio，尽管它可能不是最佳的用户体验。 不能保证所有方面都可用于低于 1280x720 的分辨率。

- 视觉工作室的目标分辨率为**1366x768。** 这是我们承诺*获得良好*用户体验的最低分辨率。

- 初始对话框高度应**小于 700 像素**，因此适合在 96 dpi 处的 IDE 帧的最小分辨率。

### <a name="high-density-displays"></a>高密度显示器
 可视化工作室中的 UI 必须在 Windows 支持开箱即用的所有 DPI 缩放因素中很好地工作：150%、200% 和 250%。

## <a name="anti-patterns"></a>若干反模式
 Visual Studio 包含许多遵循我们指南和最佳实践的 UI 示例。 为了保持一致，开发人员通常借用与构建的产品 UI 设计模式类似的产品 UI 设计模式。 尽管这是一种帮助我们在用户交互和可视化设计中保持一致性的好方法，但由于进度限制或缺陷优先级，我们偶尔会提供一些不符合我们准则的详细信息。 在这些情况下，我们不希望团队复制这些"反模式"之一，因为它们在 Visual Studio 环境中激增了坏或不一致的 UI。

### <a name="required-fieldssettings-shown-in-error-state-by-default"></a>默认情况下以错误状态显示所需的字段/设置

#### <a name="feature-team-goals"></a>功能团队目标

- 警告用户他们已添加必须配置的元素。

- 将用户的注意力吸引到需要输入的区域。

#### <a name="anti-pattern-solution"></a>反模式解决方案
 用户一旦启动操作并在完成任务之前，立即将关键停止图标放在需要配置的区域旁边。

#### <a name="example-manifest-designer-declarations"></a>示例：清单设计器声明
 向列表中添加声明会立即将其置于错误状态，该状态将一直持续到用户设置所需的属性。

 在这种情况下，还有一个额外的问题，因为用于警报的图标包含一个""&times;图标，因此不能使用常见的删除图标。 因此，UI 使用"删除"按钮，这是一个更笨重的控件。

 ![默认情况下，将 UI 置于错误状态是可视化工作室反模式。](../../extensibility/ux-guidelines/media/manifestdesignererrordeclarationsanti-pattern.png "清单设计错误声明反模式")<br />默认情况下，将 UI 置于错误状态是可视化工作室反模式。

#### <a name="alternatives"></a>备选项

解决这个问题的更好解决方案是：

- 允许用户添加声明而不发出警告，然后立即移动以设置项上的属性。

- 当焦点从项目移动时添加警告图标（金三角形），例如向列表中添加其他声明或尝试更改设计器中的选项卡。

- 如果用户尝试在任何声明上设置属性之前更改选项卡，请弹出一个对话框，解释在警告解决之前，应用程序不会生成（或任何含义）。 如果用户无论如何都会关闭对话框并更改选项卡，则图标（严重或警告，视情况而定）将添加到"声明"选项卡中。

### <a name="multiple-clicks-to-dismiss-ui"></a>多次单击以关闭 UI

#### <a name="feature-team-goals"></a>功能团队目标
 不允许用户在未首先看到说明文本的情况下关闭 UI。

#### <a name="anti-pattern"></a>反模式
 将视频链接插入 VS UI 中各个位置的团队根据 UX 指定的"关闭按钮和&times;工具提示说明"的常见模式决定，而是实现了下拉和"不再显示"链接。

#### <a name="example-video-links-in-team-explorer"></a>示例：团队资源管理器中的视频链接
强制用户在关闭 UI 之前阅读解释性文本是 Visual Studio 中的反模式。 设计正确时，视频链接应显示一个工具提示，其中包含有关悬停的其他信息，单击&times;""应无需进一步交互即可关闭消息。

 ![解释性文本反&#45;模式&#45;不正确](../../extensibility/ux-guidelines/media/incorrectuseofmultipleclicks.png "多次点击使用不正确")<br />视频链接模式不正确

用户被迫使用两次单击，只需在视频链接出现的每个位置关闭 UI，而不是简单的关闭按钮（一次单击）。

这种情况的正确设计是遵循 Internet 资源管理器、Office 和 Visual Studio 共有的模式：在悬停时，用户可以看到工具提示说明，一键隐藏 UI。

 ![解释性文本反&#45;图案&#45;正确](../../extensibility/ux-guidelines/media/explanatorytextanti-pattern-correct.png "解释性-模式-正确")<br />正确的视频链接模式

### <a name="using-command-bars-for-settings"></a>使用命令栏进行设置

**图 A**表示此反模式：在命令按钮下方放置一个设置，该设置不仅适用于命令。 在此草图中，除了"开始调试"之外，还有一些命令（如浏览器中的视图、不调试的启动和"进入"）将尊重所选设置。

![图 A：命令栏反模式](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurea.png "命令巴兰蒂模式-图")<br />图 A：命令栏反模式

稍微好一点，但仍然不可取，是把这种类型的设置在工具栏中，如图**B**所示。虽然拆分按钮占用的空间较少，因此比下拉列表改进，但两种设计仍在使用工具栏来推广实际上不是命令的内容。

![图 B：更好，但仍是命令栏反模式](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figureb.png "命令巴兰蒂模式-图B")<br />图 B：更好，但仍是命令栏反模式

在**图 C**所示的正确方法中，该设置与一系列命令相关联。 没有设置全局设置，我们只是在四个命令之间切换。 这是工具栏中命令可接受的唯一情况。

![图 C：正确使用可视化工作室命令栏模式](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurec.png "命令巴兰蒂模式-图C")<br />图 C：正确使用可视化工作室命令栏模式

### <a name="control-anti-patterns"></a>控制反模式
 某些反模式只是控件或控件组的使用或表示不正确。

#### <a name="underlining-used-as-a-group-label-not-a-hyperlink"></a>下划线用作组标签，而不是超链接
 下划线文本应仅用于超链接。

 **坏：**\
 ![非超链接的带下划线文本是可视化工作室反模式。](../../extensibility/ux-guidelines/media/0102-g_grouplabelincorrect.png "0102-g_GroupLabelIncorrect")<br />非超链接的带下划线文本是可视化工作室反模式。

 **好：**\
 ![设置正确，非超链接文本在环境字体中显示为未修饰。](../../extensibility/ux-guidelines/media/0102-h_grouplabelcorrect.png "0102-h_GroupLabelCorrect")<br />设置正确，非超链接文本在环境字体中显示为未修饰。

#### <a name="clicking-on-a-check-box-results-in-a-pop-up-dialog"></a>单击复选框会导致弹出对话框
 单击"发布 Windows Azure 应用程序"向导中的"为所有角色启用远程桌面"复选框，立即弹出一个对话框，即 Visual Studio 反模式。 此外，选中后，复选框字段不会填充复选框，这是另一个交互反模式。

 ![单击复选框后启动对话框是可视化工作室反模式。](../../extensibility/ux-guidelines/media/0102-i_checkboxpopup.png "0102-i_CheckboxPopup")<br />单击复选框后启动对话框是可视化工作室反模式。

### <a name="hyperlink-anti-patterns"></a>超链接反模式
 以下示例包含两个反模式：

1. 悬停时打开红色的前景表示不使用字体服务中的正确共享颜色。

2. "了解更多"不是指向概念主题的链接的适当文本。 用户的目标不是了解更多，它是了解他们选择的后果。

   ![忽略颜色服务并使用"了解更多"的超链接是 Visual Studio 反模式。](../../extensibility/ux-guidelines/media/0102-j_hyperlinkincorrect.png "0102-j_HyperlinkIncorrect")<br />忽略颜色服务并使用"了解更多"的超链接是 Visual Studio 反模式。

**更好的解决方案：** 通过单击链接提出用户提出的问题。 例如：

- Windows Azure 服务如何工作？

- 何时需要 Windows Azure 移动服务项目？

#### <a name="using-click-here-for-links"></a>使用"单击此处"查看链接
 超链接应具有自我描述性。 它是一种反模式，使用"点击这里"或任何类似的变化。

 **错误：**"单击此处了解有关如何创建新项目的说明。

 **良好：**"如何创建新项目？"
