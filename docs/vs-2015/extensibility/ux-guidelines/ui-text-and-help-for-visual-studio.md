---
title: UI 文本和帮助
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: e8747d07-6c90-46cc-b425-55b589f7e9e4
caps.latest.revision: 3
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ea4f2b49838340fcee41bc9c41ef94558e44825e
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67823613"
---
# <a name="ui-text-and-help-for-visual-studio"></a>UI 文本和 Visual Studio 的帮助
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="BKMK_UITextAndTerminology"></a> UI 文本和术语
 易于理解的文本对有效 UI 至关重要。 软件用户倾向于读取标签第一次，即那些最相关的完成手头的任务。 静态文本时读取更少的频率。 为用户启动他们的工作会话一次快速扫描的整个窗口中后, 跟此大致顺序 UI 的读取与制定计划：

1. 在中心的交互控件

2. 提交按钮

3. 在其他位置找到的交互控件

4. 主要说明

5. 补充说明

6. 窗口标题

7. 在正文中其他静态文本

### <a name="usage-patterns-for-ui-text"></a>UI 文本的使用模式

#### <a name="title-bar-text"></a>标题栏文本
 标题栏文本必须与匹配生成用户界面的命令。

#### <a name="instructional-text-helper-text"></a>说明文本 （帮助程序文本）
 在一些对话框中，最好提供重要的主要说明来说明要执行的操作在窗口中或在页中。 这有时称为"帮助程序文本"。

##### <a name="writing-style-rules-for-helper-text"></a>编写帮助程序文本的样式规则

- 不解释明显。 除非绝对有必要，否则不包括说明文本。

- 说明文本始终放在对话框顶部，并应参考正在执行的任务。

- 准确地向用户说明他们需要做什么。 避免过多的通信和冗余。

- 查看每个窗口，并消除重复的单词和语句。

- 保持简短的说明文本。 如果需要为某些用户或方案的详细信息，然后提供详细的概念联机主题的链接。

- 编写您的文本，使每个词保存权重，并且是必要。

- 请按照现有的 Microsoft 指南[用户界面文本](https://msdn.microsoft.com/library/windows/desktop/dn742478\(v=vs.85\).aspx)并[风格和语调](https://msdn.microsoft.com/library/windows/desktop/dn742477\(v=vs.85\).aspx)。

#### <a name="supplemental-instructions"></a>补充说明
 补充说明提供其他信息，以帮助用户了解控件或控制分组。 这可能包括了解何种格式应为输入的控件所需的提示文本。 尽量少使用补充说明。 对于用户完全不了解后果的正在进行的选择可能的情况中保留它们。

 ![在 Visual Studio 中的补充文本](../../extensibility/ux-guidelines/media/0601-b-supplementaltext1.png "0601 b_SupplementalText1")

 **在 Visual Studio 中的补充文本**

 ![在 Visual Studio 中的补充文本](../../extensibility/ux-guidelines/media/0601-c-supplementaltext2.png "0601 c_SupplementalText2")

 **在 Visual Studio 中的补充文本**

#### <a name="infotips"></a>InfoTips
 通常情况下，说明文本可能太长，在 UI 中定位的就地或可能仅向新用户，还觉得自己象混乱有经验的用户很有用。 在这种情况下，应为工具提示信息提示下放置的教学/信息性文本。

 信息提示应放置的控件，它们与相关，并且应使用尚不显眼的特定信息提示图标附近明显。

 ![在 Visual Studio 中的信息提示](../../extensibility/ux-guidelines/media/0601-d-infotip.png "0601 d_InfoTip")

 **在 Visual Studio 中的信息提示的示例**

##### <a name="writing-style-rules-for-infotips"></a>写入信息提示的样式规则

- 作为完整句子编写信息提示。 它们需要特定谓词、 句子首字母大写和结束标点。

- 使用信息提示来补充主要说明或信息。 如果只需要使用不同的词语提醒主要思路，则不需要的信息提示。

- 信息提示保持简单明了。 使用小单词和无格式、 日常语言的支持并鼓励用户。

- 请按照现有的 Microsoft 指南[用户界面文本](https://msdn.microsoft.com/library/windows/desktop/dn742478\(v=vs.85\).aspx)并[风格和语调](https://msdn.microsoft.com/library/windows/desktop/dn742477\(v=vs.85\).aspx)。

#### <a name="control-labels"></a>控件标签
 控件标签应较短的简洁，并按照[控件的 Windows 桌面指南](https://msdn.microsoft.com/library/windows/desktop/dn742399\(v=vs.85\).aspx)。

 有关控件标签格式和用户界面内的位置的详细信息，请参阅[Visual Studio 的布局](../../extensibility/ux-guidelines/layout-for-visual-studio.md)。

#### <a name="help-links"></a>帮助链接
 说明文本，文本或通过在 UI 的正文中，也可以放置帮助链接。 它们可以帮助的链接，或启动内部的对话框。

##### <a name="visual-style-rules-for-help-links"></a>帮助链接的视觉样式规则

- 使用正确的环境颜色的超链接。 正确应用了样式的超链接将不短暂地闪烁红色单击时。 如果看到此错误，则指示不使用环境颜色。

- 仅应上悬停时或当链接嵌入在段落中使用下划线。

- 超链接的视觉和交互样式的更多详细信息，请参阅按钮和超链接。

##### <a name="writing-style-rules-for-help-links"></a>编写帮助链接的样式规则

- 如果启动对话框，维护省略号的标准： 导航栏中，如果任务需要附加 UI 省略号没有省略号。

     ![在 Visual Studio 中的帮助链接](../../extensibility/ux-guidelines/media/0601-e-helplink.png "0601 e_HelpLink")

     **帮助链接中的省略号 （...） 表示任务需要附加 UI。**

- 链接应与"了解"，启动，因为这不是用户的意图。 用户想要回答特定问题，不会收到常规教育。

- 短语帮助链接，以便他们提出问题主题将解答。

     不正确：  "了解有关 Windows Azure 移动服务定价的详细信息"

     正确:  "哪些定价选项是适用于 Windows Azure 移动服务？"

- 永远不会使用*单击...* 为链接文本。

- 永远不会链接仅单词"此处"。 这是适用于某些屏幕阅读器，将语音仅超链接的 word 有问题。

     不正确：  "中找到有关 Windows Azure 移动服务**此处**"

     正确:  "哪些定价选项是适用于 Windows Azure 移动服务？"

- 正确编写样式的帮助链接的详细信息，请参阅[Windows 桌面指南以获取帮助](https://msdn.microsoft.com/library/windows/desktop/dn742494\(v=vs.85\).aspx)。

#### <a name="hint-text"></a>提示文本
 提示文本显示为水印在控件内或控件下方。 通过使用相应的 VSColors 令牌，将应用正确格式`Environment.GrayText`。

 它可以出现在多种形式。

- 代替控件标签：

     ![提示在 Visual Studio 中的文本](../../extensibility/ux-guidelines/media/0601-f-hinttext1.png "0601 f_HintText1")

- 与谓词，给出的说明：

     ![提示在 Visual Studio 中的文本](../../extensibility/ux-guidelines/media/0601-g-hinttext2.png "0601 g_HintText2")

- 使用文本，指示所需的条目：

     ![提示在 Visual Studio 中的文本](../../extensibility/ux-guidelines/media/0601-h-hinttext3.png "0601 h_HintText3")

#### <a name="watermark-text"></a>水印文本
 空设计图面上，文本应指示要执行操作，以及提供链接以打开其他相关的 windows，如果相应内容：

 ![Visual Studio 中的文本水印](../../extensibility/ux-guidelines/media/0601-i-watermarktext.png "0601 i_WatermarkText")

 **在 Visual Studio 中的水印文本的示例**

### <a name="common-terminology"></a>常见术语

|术语|说明|注释|
|----------|-----------------|-------------|
|登录/注销|使用同义词，使用 web 进行表示到 web 属性的身份验证的谓词。 在客户端，我们使用一次此作为顶级概念入和移出 IDE 用户连接，这表示提供了更高级别的功能，例如漫游和许可，不可用与所有其他连接的顶层标识签名。|IDE 用户是唯一的功能，应表示登录 / 注销谓词，因为它表示顶级 IDE 用户。|
|连接/断开连接|使用在其中一项功能会保持与联机服务的单个连接的位置。|服务器资源管理器，其中只能有一次一个活动 Azure 连接，例如连接/断开。|
|添加/删除|非破坏性。 添加或从列表中删除内容时使用。|TFS 连接管理器服务器列表对话框是添加/删除的一个示例。|
|删除|破坏性。 仅当使用将永久被丢弃或从磁盘中删除所移除的元素。|如果结果从磁盘中删除文件，"删除"通常需要一条提示。|

## <a name="error-messages"></a>错误消息

### <a name="overview"></a>概述
 错误发生。 设置限制用户可以执行的操作是合理的第一步中阻止能够避免错误消息。 但是，当确实发生错误，编写良好的错误消息可转能够大大缓解此问题。 错误消息可以说是通知的最重要的用户会看到，因为它们是通知的同步的指示需要解决的问题类型之一。 编写不佳的错误消息使用户在其自己确定错误原因和任何可能的解决方案。

 关注过度使用或混淆错误消息，因此将值添加到用户的写仅必要时邮件体验，用户可能会停止。 如果消息是只需一条通知，请使用可选表示形式。

### <a name="rules-for-creating-an-error-message"></a>创建一条错误消息的规则

- 在构造时的错误消息，为受众选择相应的错误级别。 目标提供用户所能执行，一个操作，如果适用的简单摘要。 无状态的用户无需了解任何内容。

- 提供建设性协助。 它是更轻松地读取和处理包含指令的错误消息。

- 不要使用双重否定。

- 执行这两个自动和手动的语法和拼写检查在你编写的任何错误消息。

- 对于复杂的错误消息，避免顺序通信。 永远不会使用 F1 挂钩的错误消息。 消息本身应该足够。

- 使用正确的图标。

- 使问题更易于理解和使用按钮有明确的选择，例如"删除"和"取消。

- 警告，能清楚了解继续操作的结果将是。 按钮应指示结果。

- 对于错误，描述了用户可以的操作来解决该问题。 按钮应是操作或说"关闭"。 不要使用"确定"按钮执行一条错误消息。

- 要问问自己构造一条错误消息时的一些问题：

  - 用户可以了解如何解决此错误仅出现的问题？

  - 用户是否使用与此错误相同词汇？

  - 是此错误不明确的或在多个的情况下共享？ 如果是这样，如何执行操作，引导用户到所需的解决方案？

#### <a name="build-errors"></a>生成错误
 由于 Visual Studio 是一种软件开发工具，有许多及其组件的编译时，转换，或编码步骤将开发人员的工作转换为二进制格式。 当编译器无法处理未正确编写的文件时或未正确设置编译器选项时，这些转换可能导致错误。

 Visual Studio 用户可以花费大量的开发时间解决生成错误。 此解析时间会增加错误所需的依赖项或在错误消息不佳编写，这可以使它难以发现的错误的源。

 最佳的生成错误为那些不会出现在第一个位置，这就是为什么 Visual Studio 提供了自动完成和 IntelliSense 的波形曲线。 架构验证程序和类似的工具提供相同类型的反馈。 这些机制主动指导用户构造格式正确的代码中，降低生成错误的可能性。

 Visual Studio 提供了工具窗口，用户可以读取并浏览其文档窗口中出现的错误。 键盘快捷方式提供，以便用户可以快速导航大量的代码并直接转到问题的位置。 Visual Studio 还允许以绑定到特定的帮助关键字/上下文 ID，以便用户可以直接转到更加深入地介绍有关错误的帮助主题的每个生成错误。

 编写清晰、 简洁的生成错误：

- **使用平实的语言**介绍很少或没有编译器术语中的问题。 生成错误的文本不应过于技术。

- **概述了可能的原因。** 例如，"缺少冒号之间的属性和值 （属性）: （值） 声明。"

- 提供有关可能的修补程序的详细信息。 如果没有足够的空间，更多详细信息可能会放入相应的帮助主题。

### <a name="components-of-a-well-written-error-message"></a>编写良好的错误消息的组件

#### <a name="use-the-shell-dialog-service-for-error-messages"></a>使用错误消息的外壳对话框服务。
 使用命令行程序对话框服务可让你控制消息的外观-中特定的字体，而无需对各个元素的主要更改。 使用**IErrorInfo**机制，并报告它们使用**IVsUIShell::SetErrorInfo/ReportErrorInfo**。

#### <a name="choose-an-effective-and-appropriate-notification-presentation"></a>选择一个有效且适当的通知的演示文稿。
 如果需要立即采取措施来避免丢失数据 （同步通知），请使用一个模式对话框具有严重警告。 在关闭而无需读取消息中可能会导致产生负面后果的情况下保留关键图标。 数据丢失并不需要的警报级别响应的关键情况。 严重图标的过度使用 desensitizes 用户到其重要性。 如果在本质上条信息性错误消息，请考虑一个模式对话框 （异步通知） 的替代方法。

#### <a name="provide-a-clean-succinct-explanation-of-why-the-problem-occurred-rather-than-a-technical-explanation"></a>提供而不是技术说明出现问题的原因的清晰、 简洁的说明。
 负担过重的技术详细说明中的用户将使它们更容易忽略的错误消息。 好消息传送示例：

- "无法打开请求的文件。"

- "无法连接到 Internet。"

#### <a name="provide-information-about-how-to-fix-the-problem"></a>提供有关如何解决此问题的信息。
 提供如何解决此问题的用户的建议。 坦白地讲与用户如果不有任何建议。 提供指向备用的联机源，如技术支持或社区支持的直接链接。 请尝试将用户引到特定的联机信息相关的问题。 错误 ID，请考虑将用户链接到该特定错误有关的讨论话题。 好消息传送示例：

- "请确保你连接到 Internet，然后重试此操作。"

- "请确保该文件存在并且您有权将其打开。"

#### <a name="write-a-message-that-is-short-and-to-the-point"></a>编写较短且到点的消息。
 一条错误消息可以通知，解释，并提供一个解决方案，但如果太过罗嗦仍被忽略。 一种解决方案是使用渐进式披露的详细信息按钮。 例如，为提供一个简短的说明/解决方案，然后将详细信息按钮下的更多详细信息。 如果用户选择读取错误的详细信息，用户可以这样做。

 应在消息中的语言：

- **适当域。** 使用用户将了解的语言。 尽管我们的客户都是开发人员，他们通常无上下文和我们的术语。

- **特定。** 避免含糊不清的用词并为特定的名称和所涉及对象的位置。 例如，一条错误消息如"无效字符"不是很有用。 哪些字符？ "找不到文件"。 哪些文件？

- **短暂。** 不要责怪用户，或让他们感到愚笨。 避免恶意或攻击性语言 （终止、 执行和终止，致命的非法）。 避免大写的文本，该方法通常被视为地大喊大叫并不是为可读文本。 不要使用幽默。

- **更正。** （甚至在 alpha) 中使用正确的拼写和语法。 拼写错误是不专业和令人难堪。

- **上下文相关。** 使用相应的按钮文本。 避免"确定"按钮并改为使用"继续"或"是/否。"

### <a name="error-message-examples"></a>错误消息示例

|好|错误|
|----------|---------|
|"您拨打的号码不再在服务中。 请检查数以及重试或操作员拨打 0。"|-"错误 (: 449):非法的数字"<br />-"此未经处理的异常错误情况表示操作成功完成"。<br /><br /> ![在 Visual Studio 中的严重错误消息](../../extensibility/ux-guidelines/media/0602-a-errordialog.png "0602 a_ErrorDialog")|

## <a name="accessing-help"></a>访问帮助

### <a name="overview"></a>概述
 除了 MSDN 中的文档，Visual Studio 用户具有多个访问点，以帮助用户在 UI 中。 若要确保这些访问点始终可用，功能团队需要充分利用由环境提供的帮助系统。 这些访问点是：

- **在对话框中的说明和补充性文本。** 不提供方向或说明，在 UI 图面上或可在悬停在信息提示图标上的静态文本。

- **F1 帮助**（仅编辑器）。 在 Visual Studio 编辑器中，用户可以相信，在任何时候，按 F1 会弹出一个特定于当前所选内容的帮助主题。 请确保主题与 F1 关联适当且信息丰富。

- **指向帮助主题的超链接。** 对话框、 工具窗口中或启动主题来帮助用户深入了解技术、 功能或有关如何完成某项任务的信息的设计图面内的超链接。

- **帮助器 UI 机制，例如智能标记和构建对话。** 这些机制帮助用户了解 UI 元素，或简化一个任务，例如智能标记或生成器对话框。

- **UI 帮助按钮**（不推荐使用）。 使访问相关的 F1 帮助主题的标题栏中可见的指示符。

### <a name="text"></a>Text

#### <a name="instructional-and-supplemental-text-in-dialogs"></a>在对话框中的说明和补充文本
 在支持复杂的任务的对话框，可能需要在顶部的对话框中或接近复杂的控件通常提供在 UI 中的说明文本。 请参阅[UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)有关编写样式的详细信息。

#### <a name="infotips"></a>InfoTips
 通常情况下，说明文本可能耗时较长，若要在 UI 中的位置中的位置，或者可能仅向新用户，还觉得自己象混乱有经验的用户很有用。 在这种情况下，应为工具提示信息提示下放置的教学/信息性文本。

 信息提示应放置的控件，它们与相关，并且应使用尚不显眼的特定信息提示图标附近明显。

 ![在 Visual Studio 中的信息提示](../../extensibility/ux-guidelines/media/0601-d-infotip.png "0601 d_InfoTip")

 **在 Visual Studio 中的信息提示的示例**

### <a name="interactive-help-mechanisms"></a>交互式帮助机制

#### <a name="f1-help"></a>F1 帮助
 是必需的 F1 帮助中的编辑器或设计图面上，但不是在其他位置在 Visual Studio 环境中。

#### <a name="hyperlinks-to-help-topics"></a>指向帮助主题的超链接
 超链接可用于执行的操作、 在 IDE 中导航或浏览器中启动的帮助。 请参阅[UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)有关语言和 07.10.01 的详细信息按钮和视觉对象和布局指南的超链接。

#### <a name="help--buttons-in-dialog-title-bars-deprecated"></a>帮助 [？] （已弃用） 的对话框标题栏中的按钮
 大多数情况下，不推荐使用的对话框的标题栏中的 [？] 帮助按钮。 UI 主题不再是模型的一部分我们的文档，并因此可能不会链接到相关的主题。 从根本上讲，标题栏按钮与 F1 帮助，相同的功能，不再需要的对话框中。 在某些情况下，这仍可为指示器没有概念或过程的详细信息可用，尽管在更高版本的用户界面中更常用于超链接。

##### <a name="dialogs-created-through-the-environment"></a>通过在环境创建的对话框
 通过创建的许多 shell 对话**VBDialogBoxParam**函数。 此共享的函数进行更新，以帮助移动**帮助**从到对话框按钮 **？** 按钮，同时保留体系结构，可向后兼容且可扩展。

 具体而言， **VBDialogBoxParam**函数检查其 ID 是一个按钮的对话框模板**IDHELP** (9) 或标签**帮助**或 **& 帮助**. 如果找到帮助按钮，则其处于隐藏状态和**WS_EX_CONTEXTHELP**样式添加到对话框中，放置 **？** 在对话框的标题栏中的按钮。

 创建对话框时，它将推送到堆栈上的对话框过程并使用名为预处理对话框过程调用对话框**DialogPreProc**。 当 **？** 单击按钮时，将发送**WM_SYSCOMMAND**的**SC_CONTEXTHELP**到了对话框。 **DialogPreProc**捕获此命令并将其对更改**WM_HELP**消息传递到原始对话框过程。

 大多数环境创建对话框必须在对话框的帮助按钮。 帮助按钮时显示对话框时，是自动隐藏，只有在 **？** 按钮起作用。 如果 **？** 按钮会删除或更改在 Windows 中，此解决方案，可快速将移回原始的帮助按钮。

 此解决方案进行可能会导致 bug 的四个假设：

- 在对话框的帮助按钮是**IDHELP** (9)。

- 隐藏帮助按钮时，对话框看起来正确。

- 该对话框不能将替换其 winproc。

- 对话框中未嵌入在另一个对话框。

  如果您的对话框位于 msenv 内，但不使用**VBDialogBoxParam**，调查利用**VBDialogBoxParam**实现自己的处理程序之前。

##### <a name="dialogs-created-through-other-packages"></a>通过其他包创建的对话框
 您可以实现你自己的解决方案位于外部 msenv 的对话框。 你的 VSPackage 中的共享的对话框类，请考虑移到标题栏按钮或在每个对话框实现一个处理程序。 下面的代码是实现以帮助您入门的骨架：

```
struct DLGPROCITEM
{
    FARPROC proc; // The info used to create the dialog.
    DLGPROCITEM* procPrev;
};

DLGPROCITEM* g_dlgProcStack = NULL;

// A dialog starter/wrapper function is used to push the new
// dialog proc to the top of our dialog proc stack.

int SomeDialogStarterFunction(hinst, id, proc, etc)
{
    if (g_dlgProcStack == NULL)
    {
        g_dlgProcStack = new DLGPROCITEM;
        g_dlgProcStack->procPrev = NULL;
    }
    else
    {
        DLGPROCITEM* procItem = new DLGPROCITEM;
        g_dlgProcStack->procPrev = g_dlgProcStack;
        g_dlgProcStack = procItem;
    }
}

// Pop this dialog proc off the dialog proc stack.

DialogBoxIndirectParam...(...)
{
    DLGPROCITEM* procItem = g_dlgProcStack->procPrev;
    delete g_dlgProcStack;
    g_dlgProcStack = procItem;
}

// A wrapper dialog procedure will allow us to capture the
// SC_CONTEXTHELP button on the title bar from Windows and
// forward it as a simple WM_HELP message back to the dialog.

INT_PTR CALLBACK DialogPreProc(HWND hwndDlg, UINT uMsg,
    WPARAM wParam, LPARAM lParam)
{
    if (uMsg == WM_SYSCOMMAND && wParam == SC_CONTEXTHELP)
    {
        uMsg = WM_HELP;
        wParam = 0;
        lParam = 0;
    }
    return CallWindowProc((WNDPROC)g_dlgProcStack->proc,
        hwndDlg, uMsg, wParam, lParam);
}
```

##### <a name="help-buttons-in-managed-code"></a>在托管代码中的帮助按钮
 重写窗口标题栏帮助按钮的默认行为是在托管代码中轻松。 下面是演示此行为的完整的演示应用程序。 从本质上讲，您需要重写窗体的**WndProc**方法，然后触发关闭的 F1 帮助请求时**SC_CONTEXTHELP**截获的消息。

```
using System;
using System.Windows.Forms;

public class HelpForm : Form
{
    private const int SC_CONTEXTHELP = 0xF180;
    private const int WM_SYSCOMMAND = 0x0112;

    public HelpForm()
    {
        this.ClientSize = new System.Drawing.Size(300, 250);
        this.HelpButton = true;
        this.MaximizeBox = false;
        this.MinimizeBox = false;
        this.Name = "HelpForm";
        this.Text = "Help Form";
    }

    protected override void WndProc(ref Message m)
    {
        if (m.Msg == WM_SYSCOMMAND && SC_CONTEXTHELP == (int)m.WParam)
            ShowHelp();
        else
            base.WndProc(ref m);
    }

    private void ShowHelp()
    {
        MessageBox.Show("F1 Help goes here.");
    }

     [STAThread]
    static void Main()
    {
        Application.EnableVisualStyles();
        Application.EnableRTLMirroring();
        Application.Run(new HelpForm());
    }
}
```

## <a name="see-also"></a>请参阅
 [Visual Studio 的字体和格式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md) [Visual Studio 的布局](../../extensibility/ux-guidelines/layout-for-visual-studio.md) [Visual Studio 的通知和进度](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)
