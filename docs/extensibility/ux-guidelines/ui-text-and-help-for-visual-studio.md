---
title: 可视化工作室的 UI 文本和帮助 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: e8747d07-6c90-46cc-b425-55b589f7e9e4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c0477a0e1994e9c3b94df13ace4c1f3b4df51039
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301535"
---
# <a name="ui-text-and-help-for-visual-studio"></a>Visual Studio 的 UI 文本和帮助
## <a name="ui-text-and-terminology"></a><a name="BKMK_UITextAndTerminology"></a>UI 文本和术语
 可理解的文本对于有效的 UI 至关重要。 软件用户倾向于首先阅读标签，即与完成手头任务最相关的标签。 读取静态文本的频率较低。 计划用户通过对整个窗口进行快速扫描来开始其工作会话，然后按以下近似顺序读取 UI：

1. 中间的交互式控件

2. 提交按钮

3. 在其他地方找到的交互式控件

4. 主要说明

5. 补充说明

6. 窗口标题

7. 主体中的其他静态文本

### <a name="usage-patterns-for-ui-text"></a>UI 文本的使用模式

#### <a name="title-bar-text"></a>标题栏文本
 标题栏文本必须与生成 UI 的命令匹配。

#### <a name="instructional-text-helper-text"></a>教学文本（帮助文本）
 在某些对话框中，提供突出显示的主要说明来解释在窗口或页面中应该怎么做是很有帮助的。 这有时称为"帮助者文本"。

##### <a name="writing-style-rules-for-helper-text"></a>帮助器文本的编写样式规则

- 不要解释显而易见的事实。 除非绝对需要，否则不要包含教学文本。

- 指令文本始终放在对话框的顶部，并应引用正在执行的任务。

- 向用户准确解释他们需要做什么。 避免过多的沟通和冗余。

- 查看每个窗口并消除重复的单词和语句。

- 保持教学文本简短。 如果某些用户或方案需要更多信息，则提供指向详细概念联机主题的链接。

- 写你的课文，使每个单词都保持重量，是必要的。

- 按照现有的微软用户界面[文本](/windows/desktop/uxguide/text-ui)和[样式和色调](/windows/desktop/uxguide/text-style-tone)的指导。

#### <a name="supplemental-instructions"></a>补充说明
 补充说明提供了其他信息，可帮助用户了解控件或控制分组。 这还可能包括必要的提示文本，以了解输入控件所需的格式。 请谨慎使用补充说明。 保留它们，以便用户可能无法完全理解他们做出的选择的后果。

 ![Visual Studio 中的补充文本](../../extensibility/ux-guidelines/media/0601-b_supplementaltext1.png "0601-b_SupplementalText1")

 **Visual Studio 中的补充文本**

 ![Visual Studio 中的补充文本](../../extensibility/ux-guidelines/media/0601-c_supplementaltext2.png "0601-c_SupplementalText2")

 **Visual Studio 中的补充文本**

#### <a name="infotips"></a>信息提示
 通常，指令性文本可能太长，无法将位置放在 UI 中，或者可能仅对新用户有用，对有经验的用户来说，这感觉杂乱无章。 在这种情况下，教学/信息文本应作为工具提示放置在 InfoTip 下。

 InfoTips 应放置在它们相关的控件附近，并且应该使用特定的 InfoTip 图标，该图标不显眼但明显。

 ![Visual Studio 中的信息提示](../../extensibility/ux-guidelines/media/0601-d_infotip.png "0601-d_InfoTip")

 **可视化工作室中的信息提示示例**

##### <a name="writing-style-rules-for-infotips"></a>为信息提示编写样式规则

- 将信息提示写成完整的句子。 它们需要特定的动词、句子大小写和结束标点符号。

- 使用信息提示补充您的主要说明或信息。 如果您只是使用不同的词来重提主要想法，则不需要 InfoTip。

- 保持信息提示简短而甜美。 使用支持和鼓励用户的小单词和普通的日常语言。

- 按照现有的微软用户界面[文本](/windows/desktop/uxguide/text-ui)和[样式和色调](/windows/desktop/uxguide/text-style-tone)的指导。

#### <a name="control-labels"></a>控制标签
 控件标签应简短、简洁，并遵循[控件的 Windows 桌面指南](/windows/desktop/uxguide/controls)。

 有关控件标签格式和在 UI 中放置的详细信息，请参阅[可视化工作室的布局](../../extensibility/ux-guidelines/layout-for-visual-studio.md)。

#### <a name="help-links"></a>“帮助”链接
 帮助链接可以放置在教学文本中或 UI 正文中。 它们可以是指向"帮助"或"启动内部对话框"的链接。

##### <a name="visual-style-rules-for-help-links"></a>帮助链接的可视样式规则

- 对超链接使用正确的环境颜色。 正确样式的超链接在单击时不会短暂闪烁红色。 如果看到这一点，则表示未使用环境颜色。

- 下划线应仅在悬停或链接嵌入段落时使用。

- 有关超链接的可视样式和交互样式的更多详细信息，请参阅按钮和超链接。

##### <a name="writing-style-rules-for-help-links"></a>为帮助链接编写样式规则

- 启动对话框时，维护椭圆的标准：没有用于导航的椭圆，如果任务需要额外的 UI，则省略号。

     ![Visual Studio 中的帮助链接](../../extensibility/ux-guidelines/media/0601-e_helplink.png "0601-e_HelpLink")

     **帮助链接中的省略号 （...） 表示任务将需要其他 UI。**

- 链接不应以"学习"开头，因为这不是用户的意图。 用户希望回答特定问题，而不是接受普通教育。

- 短语帮助链接，以便他们提出主题将回答的问题。

     不正确："了解有关 Windows Azure 移动服务定价的更多信息"

     正确："Windows Azure 移动服务有哪些定价选项？

- 切勿使用 *"单击..."* 链接文本。

- 切勿只链接"此处"一词。 这对某些屏幕阅读器来说是个问题，因为屏幕阅读器将只发出超链接单词的语音。

     不正确："**在此处**查找 Windows Azure 移动服务的信息"

     正确："Windows Azure 移动服务有哪些定价选项？

- 有关帮助链接的正确书写样式的详细信息，请参阅["帮助"的 Windows 桌面指南](/windows/desktop/uxguide/winenv-help)。

#### <a name="hint-text"></a>提示文本
 提示文本在控件内或控件下方显示为水印。 将使用相应的 VSColors 令牌应用正确的格式`Environment.GrayText`。

 它可以以多种形式显示。

- 代替控制标签：

     ![Visual Studio 中的提示文本](../../extensibility/ux-guidelines/media/0601-f_hinttext1.png "0601-f_HintText1")

- 用动词，给出指示：

     ![Visual Studio 中的提示文本](../../extensibility/ux-guidelines/media/0601-g_hinttext2.png "0601-g_HintText2")

- 文本指示必需的条目：

     ![Visual Studio 中的提示文本](../../extensibility/ux-guidelines/media/0601-h_hinttext3.png "0601-h_HintText3")

#### <a name="watermark-text"></a>水印文本
 在空的设计图面上，文本应指明要执行哪些操作，并提供适当的链接以打开其他相关窗口：

 ![Visual Studio 中的水印文本](../../extensibility/ux-guidelines/media/0601-i_watermarktext.png "0601-i_WatermarkText")

 **视觉工作室中的水印文本示例**

### <a name="common-terminology"></a>常用术语

|术语|说明|注释|
|----------|-----------------|-------------|
|登录/注销|动词与 Web 同义用于表示 Web 属性中的身份验证。 在客户端中，我们一次使用此概念作为登录和注销 IDE 用户连接的顶级概念，该概念表示提供更高级别的功能（如漫游和许可）的顶级标识，而所有其他连接都不可用。|IDE 用户是唯一应表示登录/注销谓词的功能，因为它表示顶级 IDE 用户。|
|连接/断开连接|用于功能与联机服务保持单个连接的位置。|服务器资源管理器（一次只能有一个活动 Azure 连接）是连接/断开连接的示例。|
|添加/删除|无损。 从列表中添加或删除内容时使用。|TFS 连接管理器服务器列表对话框是添加/删除的示例。|
|删除|破坏性。 仅当要删除的元素将被永久丢弃或从磁盘中删除时，才使用。|如果结果从磁盘中删除文件，则"删除"通常需要提示。|

## <a name="error-messages"></a>错误消息

### <a name="overview"></a>概述
 会发生错误。 设置用户可以做什么的限制是防止可避免错误消息的明智第一步。 但是，当发生错误时，编写良好的错误消息可以很好地缓解问题。 错误消息可以说是用户看到的最重要通知类型之一，因为它们是同步的，并且指示需要解决的问题。 编写不良的错误消息使用户自行决定错误的原因和任何可能的解决方案。

 用户可能会停止关注过度使用或混淆的错误消息，因此只编写为用户体验增加价值的必要消息。 如果消息只是通知，则使用备用演示文稿。

### <a name="rules-for-creating-an-error-message"></a>创建错误消息的规则

- 构造错误消息时，为访问群体选择适当的错误级别。 旨在获取提供用户可以执行的操作（如果适用）的简单摘要。 不要说明用户不需要知道的任何内容。

- 提供建设性援助。 阅读和操作包含指令的错误消息更容易。

- 不要使用双底片。

- 对您编写的任何错误消息执行自动和手动语法和拼写检查。

- 对于复杂的错误消息，请避免顺序通信。 切勿对错误消息使用 F1 连接。 消息本身应足够。

- 使用正确的图标。

- 使问题易于理解，并使用具有明确选择的按钮，如"删除"和"取消"。

- 对于警告，要明确操作的后果。 按钮应指示结果。

- 对于错误，请描述用户可以采取哪些措施来解决此问题。 按钮应该是操作或说"关闭"。 不要对错误消息使用"确定"按钮。

- 构造错误消息时要问自己的一些问题：

  - 用户能否单独找出如何仅使用此错误解决问题？

  - 用户是否使用此与此错误相同的词汇表？

  - 此错误是大错还是在多种情况下共享？ 如果是，您如何引导用户找到他们需要的解决方案？

#### <a name="build-errors"></a>生成错误
 由于 Visual Studio 是一个软件开发工具，因此其许多组件都有编译、转换或编码步骤，可将开发人员的工作转换为二进制形式。 当编译器无法处理创作不当的文件或编译器选项设置不正确时，这些转换可能会导致错误。

 Visual Studio 用户可以花费大量开发时间来解决生成错误。 当错误具有依赖关系或错误消息写得不好时，此解决时间会增加，这会使发现错误源变得困难。

 最好的生成错误是那些首先不会发生的错误，这就是为什么 Visual Studio 提供自动完成和 IntelliSense 摆动的原因。 架构验证器和类似的工具提供相同类型的反馈。 这些机制主动引导用户构建格式良好的代码，从而减少生成错误的可能性。

 Visual Studio 提供了一个工具窗口，用户可以在其中读取和导航其文档窗口中发生的错误。 提供键盘快捷键，以便用户可以快速导航大量代码并直接转到问题的位置。 Visual Studio 还允许将每个生成错误绑定到特定的帮助关键字/上下文 ID，以便用户可以直接转到"帮助"主题，该主题提供有关该错误的更深入信息。

 编写清晰、简洁的生成错误：

- **使用简单的语言**来解释问题，很少或没有编译器行话。 生成错误的文本不应过于技术化。

- **概述可能的原因。** 例如，"在 '（属性）：（值）'声明中的属性和值之间缺少一个冒号。

- 提供有关潜在修复的详细信息。 如果没有足够的空间，则其他详细信息可能会放入相应的帮助主题中。

### <a name="components-of-a-well-written-error-message"></a>写得很好的错误消息的组件

#### <a name="use-the-shell-dialog-service-for-error-messages"></a>对错误消息使用 shell 对话框服务。
 使用 shell 对话框服务可以控制消息的外观，尤其是字体，而无需对单个元素进行重大更改。 使用**IErrorInfo**机制并使用**IVsUIShell：：设置ErrorInfo/报告错误信息**报告它们。

#### <a name="choose-an-effective-and-appropriate-notification-presentation"></a>选择有效和适当的通知演示文稿。
 如果需要立即采取行动以避免数据丢失（同步通知），请使用带有严重警告的模态对话框。 关键图标保留用于在不阅读消息的情况下关闭邮件可能会导致负面后果的情况。 数据丢失是需要报警级响应的危急情况。 过度使用关键图标会使用户对其重要性失去敏感性。 如果错误消息具有信息性，请考虑模式对话框（异步通知）的替代方法。

#### <a name="provide-a-clean-succinct-explanation-of-why-the-problem-occurred-rather-than-a-technical-explanation"></a>提供清晰、简洁的解释，说明问题发生的原因，而不是技术解释。
 在解释中给用户带来技术细节负担过重会使他们更有可能忽略错误消息。 良好消息传递的示例：

- 无法打开请求的文件。

- "无法连接到互联网。

#### <a name="provide-information-about-how-to-fix-the-problem"></a>提供有关如何解决此问题的信息。
 为用户提供如何解决此问题的建议。 如果没有建议，要诚实地对待用户。 提供指向其他在线来源的直接链接，例如技术支持或社区支持。 尝试将用户指向与问题相关的特定联机信息。 对于错误 ID，请考虑将用户链接到有关该特定错误的讨论线程。 良好消息传递的示例：

- "请确保您已连接到互联网，然后重试此操作。

- 确保文件存在，并且您有权打开该文件。

#### <a name="write-a-message-that-is-short-and-to-the-point"></a>写一条简短而正确的消息。
 错误消息可以通知、解释和提供解决方案，但如果过于措辞，仍被忽略。 一种解决方案是使用带有详细信息按钮的渐进式披露。 例如，给出一个简短的描述/解决方案，然后将更多详细信息放在详细信息按钮下。 如果用户选择阅读有关该错误的详细信息，则可以这样做。

 消息中的语言应为：

- **适合域。** 使用用户将理解的语言。 尽管我们的客户是开发人员，但他们通常没有我们的上下文和术语。

- **特定。** 避免措辞模糊，并给出所涉物体的具体名称和位置。 例如，错误消息（如"字符无效"）没有用处。 哪个角色？ "找不到文件。 哪个文件？

- **礼貌。** 不要责怪用户或让他们感到愚蠢。 避免使用敌对或冒犯性语言（杀戮、执行、终止、致命、非法）。 避免大写文本，这通常被视为喊话，并且不可读。 不要用幽默。

- **正确。** 使用正确的拼写和语法（即使在 alphas 中）。 泰波斯是不专业和尴尬的。

- **上下文适当。** 使用适当的按钮文本。 避免使用"确定"按钮，而是使用"继续"或"是/否"。

### <a name="error-message-examples"></a>错误消息示例

|好|糟糕|
|----------|---------|
|您拨打的号码不再在服务中。 请检查该号码并再次拨号，或拨打 0 的接线员。|- "错误 （449）： 非法号码"<br />- "此未处理的异常错误表示操作成功完成。<br /><br /> ![Visual Studio 中的严重错误消息](../../extensibility/ux-guidelines/media/0602-a_errordialog.png "0602-a_ErrorDialog")|

## <a name="accessing-help"></a>访问帮助

### <a name="overview"></a>概述
 除了 MSDN 中的文档之外，Visual Studio 用户还有多个接入点在 UI 中帮助用户。 为了确保这些接入点始终可用，功能团队需要利用环境提供的帮助系统。 这些接入点包括：

- **对话框中的教学和补充文本。** 在 UI 表面上提供方向或说明的静态文本，或在 InfoTip 图标上可用。

- **F1 帮助**（仅限编辑器）。 在 Visual Studio 编辑器中，用户可以相信，在任何时候都按 F1 将显示特定于当前选择的帮助主题。 确保与 F1 相关的主题是适当且内容丰富的。

- **指向帮助主题的超链接。** 对话框、工具窗口或设计图面中的超链接，用于启动主题，以帮助用户了解有关如何完成任务的技术、功能或信息的详细信息。

- **帮助器 UI 机制，如智能标记和生成对话框。** 这些机制可帮助用户了解 UI 元素，或促进任务（如智能标记或生成器对话框）。

- **UI 帮助按钮**（已弃用）。 标题栏中允许访问相关 F1 帮助主题的可见指示器。

### <a name="text"></a>文本

#### <a name="instructional-and-supplemental-text-in-dialogs"></a>对话框中的教学和补充文本
 在支持复杂任务的对话框中，可能需要在 UI 中（通常在对话框顶部或复杂控件附近）提供指令文本。 有关书写样式的详细信息，请参阅[UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)。

#### <a name="infotips"></a>信息提示
 通常，指令性文本可能太长，无法在 UI 中定位，或者可能仅对新用户有用，对有经验的用户来说，感觉杂乱无章。 在这种情况下，教学/信息文本应作为工具提示放置在 InfoTip 下。

 InfoTips 应放置在它们相关的控件附近，并且应该使用特定的 InfoTip 图标，该图标不显眼但明显。

 ![Visual Studio 中的信息提示](../../extensibility/ux-guidelines/media/0601-d_infotip.png "0601-d_InfoTip")

 **可视化工作室中的信息提示示例**

### <a name="interactive-help-mechanisms"></a>交互式帮助机制

#### <a name="f1-help"></a>F1 帮助
 F1 帮助在编辑器或设计图面中是必需的，但在可视化工作室环境中的其他位置则不需要 F1 帮助。

#### <a name="hyperlinks-to-help-topics"></a>指向帮助主题的超链接
 超链接可用于在 IDE 中执行操作、在 IDE 中导航或在浏览器中启动帮助。 有关语言和 07.10.01 按钮和超链接的详细信息，请参阅[UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)，了解可视化和布局指南。

#### <a name="help--buttons-in-dialog-title-bars-deprecated"></a>对话框标题栏中的帮助 [？] 按钮（已弃用）
 在大多数情况下，对话框标题栏中的"帮助"按钮将被弃用。 UI 主题不再是文档模型的一部分，因此可能没有要链接到的相关主题。 从本质上讲，标题栏按钮与 F1 帮助相同，在对话框中不再需要。 在某些情况下，这仍可用作可用更多概念或过程信息的指示器，尽管超链接在较新的 UI 中更常用。

##### <a name="dialogs-created-through-the-environment"></a>通过环境创建的对话框
 许多 shell 对话框都是通过**VBDialogBoxParam**函数创建的。 此共享函数已更新，以帮助将 **"帮助"** 按钮从对话框移动到 **"** 按钮，同时保留向后兼容和可扩展的体系结构。

 具体来说 **，VBDialogBoxParam**函数查看一个按钮的对话框模板，该按钮的**IDHELP** （9） 或标签是 **"帮助**"或 **"帮助"&**。 如果找到"帮助"按钮，则该按钮将隐藏，**并将WS_EX_CONTEXTHELP**样式添加到对话框中，对话框中放置**了 "帮助"按钮。** 对话框标题栏中的按钮。

 创建对话框时，它会将对话框进程推送到堆栈上，并调用对话框，预处理对话框进程名为**DialogPreProc**。 何时 **？** 单击按钮，它将**SC_CONTEXTHELPWM_SYSCOMMAND**发送到对话框**WM_SYSCOMMAND**。 **DialogPreProc**捕获此命令并将其更改为**WM_HELP**消息，该消息将传递到原始对话框进程。

 大多数环境创建的对话框在对话框上都有"帮助"按钮。 显示对话框时，"帮助"按钮将自动隐藏，并且仅隐藏 **"帮助"按钮。** 按钮工作正常。 如果 **？** 按钮在 Windows 中被删除或更改，此解决方案允许您快速移回原始帮助按钮。

 此解决方案会做出四种可能导致 bug 的假设：

- 对话框的帮助按钮是**IDHELP** （9）。

- 隐藏"帮助"按钮时，该对话框看起来正确。

- 该对话框不能替换其 winproc。

- 对话框未嵌入到另一个对话框中。

  如果对话框位于 msenv 中，并且不使用**VBDialogBoxParam，** 请先调查利用**VBDialogBoxParam，** 然后再实现您自己的处理程序。

##### <a name="dialogs-created-through-other-packages"></a>通过其他包创建的对话框
 您可以为驻留在 msenv 外部的对话框实现自己的解决方案。 对于 VSPackage 中的共享对话框类，请考虑将按钮移动到标题栏或在每个对话框上实现处理程序。 以下代码是实现的框架，可帮助您入门：

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

##### <a name="help-buttons-in-managed-code"></a>托管代码中的帮助按钮
 在托管代码中，重写窗口标题栏"帮助"按钮的默认行为非常简单。 下面是演示此行为的完整演示应用程序。 从本质上讲，您需要重写表单的**WndProc**方法，然后在截获**SC_CONTEXTHELP**消息时触发 F1 帮助请求。

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

## <a name="see-also"></a>另请参阅
- [Visual Studio 的字体和格式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)
- [Visual Studio 的布局](../../extensibility/ux-guidelines/layout-for-visual-studio.md)
- [Visual Studio 的通知和进度](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)
