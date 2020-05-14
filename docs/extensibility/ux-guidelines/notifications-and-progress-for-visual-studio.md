---
title: 视觉工作室的通知和进度 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f0ef65e9-0f1f-45f4-9f25-6e2398691168
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5f6a7ddd5d1a5a7257617b03098722e1341017b6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699887"
---
# <a name="notifications-and-progress-for-visual-studio"></a>Visual Studio 的通知和进度
## <a name="notification-systems"></a><a name="BKMK_NotificationSystems"></a>通知系统

### <a name="overview"></a>概述
 有几种方法可以告知用户 Visual Studio 中有关其软件开发任务的情况。

 实现任何类型的通知时：

- **将通知数保持在最小**有效数量。 通知消息应应用于大多数 Visual Studio 用户或特定功能/功能区域的用户。 过度使用通知可能会使用户感到轻松，或降低系统的易用性。

- **确保您呈现清晰、可操作的消息**，用户可以使用这些消息调用适当的上下文，以便做出更复杂的选择并采取进一步操作。

- **适当地显示同步和异步消息。** 同步通知指示某些内容需要立即关注，例如当 Web 服务崩溃或引发代码异常时。 应立即以需要输入的方式通知用户这些情况，例如在模式对话框中。 异步通知是用户应该知道的，但不需要立即执行，例如生成操作完成或网站部署完成时。 这些消息应更具环境性，而不是中断用户的任务流。

- **仅在必要时使用模态对话框，以防止用户**在确认消息或做出对话框中显示的决定之前采取进一步操作。

- **当环境通知不再有效时，请将其删除。** 如果用户已采取措施解决他们收到通知的问题，则不要要求用户关闭通知。

- **请注意，通知可能会导致错误的相关性。** 用户可能认为，他们的一个或多个行为触发了通知，而实际上没有因果关系。 在有关上下文、触发器和通知源的通知消息中要清楚。

### <a name="choosing-the-right-method"></a>选择正确的方法
 使用此表可帮助您选择正确的方法来通知用户您的消息。

|方法|使用|请勿使用|
|------------|---------|----------------|
|[模式错误消息对话框](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ModalErrorMessageDialogs)|在需要用户响应之前，在继续操作时使用。|当不需要阻止用户并中断其流时，请勿使用。 如果可以用另一种不太侵入性的方式显示消息，则避免使用模式对话框。|
|[IDE 状态栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_IDEStatusBar)|当有有关进程状态的环境文本信息时使用。|不要单独使用。 最佳与其他反馈机制结合使用。|
|[嵌入式信息栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedInfobar)|在工具窗口或文档窗口中，用于通知进度、错误状态、结果和/或可操作信息。|如果信息与放置信息栏的位置无关，请勿使用。<br /><br /> 请勿在文档/工具窗口外使用。|
|[鼠标光标更改](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_MouseCursorChanges)|可用于通知进程正在进行。 还用于通知鼠标中存在状态更改，例如拖动/放置正在进行或鼠标光标处于特定模式（如绘图模式）时。|请勿用于短期进度更改或如果可能飘动游标（例如，绑定到运行较长的进程的部分而不是整个进程）。|
|[进度指标](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotSysProgressIndicators)|当您需要报告进度（不确定或不确定）时使用。 每种进度指标类型和特定用法都有多种。 请参阅[进度指示器](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators)。||
|[Visual Studio“通知”窗口](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_VSNotificationsToolWindow)|通知窗口不可公开扩展。 但是，它用于传达有关 Visual Studio 的一系列消息，包括许可证的关键问题以及 Visual Studio 或包更新的信息性通知。|请勿用于其他类型的通知。|
|[错误列表](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ErrorList)|当问题与用户当前打开的解决方案有问题（错误/警告/信息）直接相关时，他们可能需要对代码执行操作。<br /><br /> 例如，这将包括：<br /><br /> - 编译器消息（错误/警告/信息）<br /><br /> - 代码分析器/有关代码的诊断消息<br /><br /> - 生成消息<br /><br /> 可能适用于与项目或解决方案文件相关的问题，但首先考虑解决方案资源管理器指示。|不要用于与用户打开的解决方案代码没有任何关系的项。|
|编辑器通知：灯泡|当您有可用于修复修复打开文件中存在的问题时，请使用。<br /><br /> 请注意，灯泡还应用于托管按需对用户代码执行的操作，例如重构，但在这种情况下不会出现"通知样式"。|不要用于与打开文件没有任何关系的项。|
|编辑器通知： 摇摆|用于提醒用户其打开代码的特定范围的问题（例如，错误的红色波浪）。|不要用于与其打开代码的特定范围无关的项目。|
|[嵌入式状态栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedStatusBars)|用于提供与特定工具窗口、文档窗口或对话框窗口上下文中的内容或进程相关的状态。|请勿用于与特定窗口中的内容没有任何关系的一般产品通知、流程或项目。|
|[窗口托盘通知](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_WindowsTray)|用于为进程外进程或配套应用程序显示通知。|不要用于与 IDE 相关的通知。|
|[通知气泡](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotificationBubbles)|用于通知远程进程或 IDE**外部**的更改。|请勿使用作为通知用户 IDE**中**的进程的方法。|

### <a name="notification-methods"></a>通知方法

#### <a name="modal-error-message-dialogs"></a><a name="BKMK_ModalErrorMessageDialogs"></a>模式错误消息对话框
 模式错误消息对话框用于显示需要用户确认或操作的错误消息。

 ![模式错误消息](../../extensibility/ux-guidelines/media/0901-01_modalerrormessage.png "0901-01_ModalErrorMessage")

 **向用户发出警报的无效连接字符串到数据库的模式错误消息对话框**

#### <a name="ide-status-bar"></a><a name="BKMK_IDEStatusBar"></a>IDE 状态栏
 用户注意到状态栏文本的可能性与其全面的计算机体验和 Windows 平台的特定体验相关。 Visual Studio 客户群往往在这两个方面都有经验，但即使是知识渊博的 Windows 用户也可能错过状态栏中的更改。 因此，状态栏最适合用于信息目的或作为在其他地方显示的信息的冗余提示。 用户必须立即解决的任何类型的关键信息都应在对话框中或在"通知"工具窗口中提供。

 Visual Studio 状态栏旨在允许显示多种类型的信息。 它分为反馈、设计器、进度栏、动画和客户端的区域。

 反馈区域和设计器区域始终可见。 进度栏和动画区域始终动态，并且基于用户上下文。 设计器区域具有静态宽度，由从文本消息的随附资源提取的字符串的长度决定。 这允许本地化调整宽度大小，而无需更改代码。 对于英语，此字符串的宽度约为 220 像素。 设计器区域将运行正常，反馈区域将吸收剩余空间。

 状态栏还着色，通过传达各种 IDE 状态更改（如 IDE 处于调试模式时）来增加视觉兴趣和功能值。

 ![IDE 状态栏颜色更改](../../extensibility/ux-guidelines/media/0901-02_idestatusbar.png "0901-02_IDEStatusBar")

 **IDE 状态栏颜色**

#### <a name="embedded-infobar"></a><a name="BKMK_EmbeddedInfobar"></a>嵌入式信息栏
 信息栏可以在文档窗口或工具窗口的顶部用于通知用户状态或条件。 它还可以提供命令，以便用户可以有一种轻松执行操作的方法。 信息栏是一个标准外壳控件。 避免创建自己的，这将在 IDE 中的行为和行为与其他操作不一致。 有关实现详细信息和使用指南[，请参阅信息栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)。

 ![嵌入式信息栏](../../extensibility/ux-guidelines/media/0901-03_embeddedinfobar.png "0901-03_EmbeddedInfobar")

 **嵌入在文档窗口中的信息栏，提醒用户 IDE 处于历史调试模式，编辑器的响应方式与标准调试模式不同。**

#### <a name="mouse-cursor-changes"></a><a name="BKMK_MouseCursorChanges"></a>鼠标光标更改
 更改鼠标光标时，请使用绑定到 VSColor 服务且已与光标关联的颜色。 光标更改可用于指示正在进行的操作，以及用户将鼠标悬停在可拖动、拖到或用于选择对象的目标上的命中区域。

 仅当必须为操作保留所有可用的 CPU 时间时，才使用忙/等待鼠标光标，以防止用户表示任何进一步输入。 在大多数情况下，使用多线程编写良好的应用程序时，阻止用户执行其他操作的时间应该很少。

 请记住，光标更改对于其他地方提供的信息非常有用。 不要依赖光标更改作为与用户通信的唯一方式，尤其是在尝试传达用户必须解决的关键内容时。

#### <a name="progress-indicators"></a><a name="BKMK_NotSysProgressIndicators"></a>进度指标
 进度指示器对于在需要几秒钟以上才能完成的流程期间向用户提供反馈非常重要。 进度指示器可以就地显示（靠近正在进行的操作的启动点）、嵌入式状态栏、模态对话框或 Visual Studio 状态栏。 遵循[进度指标](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators)中有关其使用和实施的指导。

#### <a name="visual-studio-notifications-window"></a><a name="BKMK_VSNotificationsToolWindow"></a>可视化工作室通知窗口
 "可视化工作室通知"窗口通知开发人员有关许可、环境（可视化工作室）、扩展和更新。 用户可以关闭单个通知，也可以选择忽略某些类型的通知。 忽略的通知列表在 **"工具>选项**"页中管理。

 通知窗口当前不可扩展。

 ![Visual Studio“通知”窗口](../../extensibility/ux-guidelines/media/0901-06_vsnotificationswindow.png "0901-06_VSNotificationsWindow")

 **可视化工作室通知工具窗口**

#### <a name="error-list"></a><a name="BKMK_ErrorList"></a>错误列表
 错误列表中的通知指示编译和生成过程中发生的错误和警告，并允许用户在代码中导航到该特定代码错误。

 ![错误列表](../../extensibility/ux-guidelines/media/0901-08_errorlist.png "0901-08_ErrorList")

 **可视化工作室中的错误列表**

#### <a name="embedded-status-bars"></a><a name="BKMK_EmbeddedStatusBars"></a>嵌入式状态栏
 由于 IDE 状态栏是动态的，其客户端区域上下文设置为活动文档窗口，并在用户的上下文和/或系统响应上更新信息，因此很难保持信息的持续显示或对长期异步进程的状态。 例如，IDE 状态栏不适用于多个运行和/或立即可操作项选择的测试运行结果通知。 请务必在用户进行选择或启动进程的文档或工具窗口的上下文中保留此类状态信息。

 ![嵌入式状态栏](../../extensibility/ux-guidelines/media/0901-09_embeddedstatusbar.png "0901-09_EmbeddedStatusBar")

 **视觉工作室中的嵌入式状态栏**

#### <a name="windows-tray-notifications"></a><a name="BKMK_WindowsTray"></a>窗口托盘通知
 Windows 通知区域位于 Windows 任务栏上的系统时钟旁边。 许多实用程序和软件组件在此区域中提供图标，以便用户可以获取系统范围任务的上下文菜单，例如更改屏幕分辨率或获取软件更新。

 环境级通知应出现在可视化工作室通知中心，而不是 Windows 通知区域。

#### <a name="notification-bubbles"></a><a name="BKMK_NotificationBubbles"></a>通知气泡
 通知气泡可以在编辑器/设计器中显示为信息，也可以显示为 Windows 通知区域的一部分。 用户将这些气泡视为以后可以解决的问题，这对非关键通知是有好处的。 气泡不适合用户必须马上解决的关键信息。 如果在 Visual Studio 中使用通知气泡，请按照[Windows 桌面指南进行通知气泡](/windows/desktop/uxguide/mess-notif)。

 ![通知气泡](../../extensibility/ux-guidelines/media/0901-07_notificationbubbles.png "0901-07_NotificationBubbles")

 **用于可视化工作室的 Windows 通知区域中的通知气泡**

## <a name="progress-indicators"></a><a name="BKMK_ProgressIndicators"></a>进度指标

### <a name="overview"></a>概述
 进度指标是通知系统向用户反馈的重要组成部分。 他们告诉用户何时完成流程和操作。 熟悉的指示器类型包括进度条、旋转光标和动画图标。 进度指标的类型和位置取决于上下文，包括报告的内容以及流程或操作完成的时间。

#### <a name="factors"></a>因素
 为了确定适合哪个指标类型，您需要确定以下因素。

1. **时间：** 操作需要多长时间

2. **模式：** 操作是否对环境模态（锁定 UI 直到该过程完成）

3. **持久/暂时性：** 是否需要在以后报告和/或查看进度的最终结果

4. **确定/不确定：** 是否可以计算操作结束时间和进度

5. **图形/文本位置：** 进度或进程是内联、消息正文中捕获还是特定控件（如树控件）

6. **邻近：** 进度是否应靠近与其相关的 UI。 （例如，它是在状态栏中（可能距离很远），还是必须靠近启动进程的按钮？）

#### <a name="determinate-progress"></a>确定进度

|进度类型|何时以及如何使用|说明|
|-------------------|-------------------------|-----------|
|进度条（确定）|预计持续时间为 >5 秒。<br /><br /> 可能包括过程详细信息的文本描述。|**不要**将文本嵌入动画中。|
|信息栏|与上下文 UI 关联的消息。 请参阅[信息栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)。<br /><br /> 可能包括过程详细信息的文本描述。|当您需要指示多个进程时，**不要**使用多个信息栏。 改用堆叠进度条。|
|输出窗口|临时通知：用户希望在完成后**查看**其详细信息的应用级进程。|如果用户以后需要参考数据，**请不要**使用。|
|日志文件|在完成后**保存**详细信息很重要的情况下，与临时通知配对。||
|状态栏|瞬态通知：用户在完成后**不需要**的详细信息的应用级进程。<br /><br /> 包括嵌入进度栏。<br /><br /> 可能包括过程详细信息的文本描述。||

#### <a name="indeterminate-progress"></a>不确定的进度

|进度类型|何时以及如何使用|说明|
|-------------------|-------------------------|-----------|
|进度条（不确定）|预计持续时间为 >5 秒。<br /><br /> 可能包括过程详细信息的文本描述。|**不要**将文本嵌入动画中。|
|蚂蚁（动画水平点）|服务器往返。<br /><br /> 放置在父容器顶部的上下文点附近。|如果不由整个容器父级，**请勿**使用。|
|微调器（进度环）|与上下文 UI 关联的进程，或空间是考虑因素的位置。<br /><br /> 可能包括过程详细信息的文本描述。||
|信息栏|与上下文 UI 关联的消息。 请参阅[信息栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)。|当您需要指示多个进程时，**不要**使用多个信息栏。 改用堆叠进度条。|
|输出窗口|临时通知：用户希望在完成后**查看**其详细信息的应用级进程。|**不要**用于需要跨会话保留的信息。|
|日志文件|在完成后**保存**详细信息很重要的情况下，与临时通知配对。||
|状态栏|瞬态通知：用户在完成后**不需要**的详细信息的应用级进程。<br /><br /> 包括嵌入式进度条。<br /><br /> 可能包括过程详细信息的文本描述。||

### <a name="progress-indicator-types"></a>进度指示器类型

#### <a name="progress-bars"></a>进度条

##### <a name="indeterminate"></a>定
 ![不确定的进度栏](../../extensibility/ux-guidelines/media/0901-04_indeterminate.png "0901-04_Indeterminate")

 **不确定的进度栏**

 "不确定"是指无法确定操作或流程的总体进度。 对需要无限时间或访问未知数量的对象的操作使用不确定的进度条。 使用文本说明来伴随正在发生的事情。 使用超时为基于时间的操作提供边界。 不确定的进度条使用动画来显示正在取得进展，但没有提供其他信息。 不要仅根据可能缺乏准确性来选择不确定的进度条。

##### <a name="determinate"></a>确定
 ![确定的进度栏](../../extensibility/ux-guidelines/media/0901-05_determinate.png "0901-05_Determinate")

 **确定的进度栏**

 "确定"是指操作或过程需要有限的时间量，即使无法准确预测该时间量。 清楚地表示已完成。 除非操作已完成，否则不要让进度条转到 100%。 确定进度条动画从左到右从 0 移动到 100%。

 切勿在操作期间向后移动进度指示器。 当操作开始时，柱线应稳步向前移动，并在操作结束时达到 100%。 进度条的要点是让用户了解整个操作需要多长时间，而不管涉及多少步骤。

##### <a name="concurrent-reporting-stacked-progress-bars"></a>并发报告（堆叠进度条）
 如果操作需要很长时间（也许几分钟），则可以使用两个进度条，一个显示操作的总体进度，另一个显示当前步骤的进度。 例如，如果安装程序正在复制许多文件，则一个进度栏可用于指示整个过程需要多长时间，而第二个进度栏可以指示正在复制当前文件或目录的百分比。 不要使用堆叠进度条报告超过五个并发操作或进程。 如果要报告五个以上并发操作或进程，请使用带有"取消"按钮的模式对话框，并将进度详细信息报告给输出窗口。

##### <a name="textual-descriptions"></a>文本描述
 使用文本说明来配合正在发生的事情和估计的完成时间。 如果无法确定操作需要多长时间，则提供反馈的更好选择可能是动画图标而不是进度栏。

 Visual Studio 在状态栏中提供了一个标准进度栏，可用于集成到 Visual Studio 的任何产品。 对于在动画处理进度栏时发生的情况的文本说明，可以更新状态栏文本。

#### <a name="other-progress-indicators"></a>其他进展指标

##### <a name="ants-animated-horizontal-dots"></a>蚂蚁（动画水平点）
 ![进度 ant](../../extensibility/ux-guidelines/media/0903-01_ants.png "0903-01_Ants")

 "Ants"，动画水平点，为不确定的往返服务器进程提供视觉参考。

##### <a name="spinner-progress-ring"></a>微调器（进度环）
 ![进度微调框](../../extensibility/ux-guidelines/media/0903-02_spinner.png "0903-02_Spinner")

 微调器（也称为"进度环"）是一个不确定的进展指示器，主要用于上下文 UI。 显示与其相关内容（如文本类别标题、消息传递或控件）非常接近的微调器。

##### <a name="cursor-feedback"></a>光标反馈
 对于需要 2-7 秒的操作，提供光标反馈。 通常，这意味着使用操作系统提供的等待光标。 有关指导，请参阅 MSDN 文章[Cursors.Wait 属性](/dotnet/api/system.windows.input.cursors.wait)。

#### <a name="progress-indicator-locations"></a>进度指示器位置

##### <a name="status-bar"></a>状态栏
 状态栏为应用程序提供了在不中断用户工作的情况下向用户显示消息和有用信息的位置。 通常显示在窗口底部，进度状态将是一个工具提示窗格，其中包含有关进度度量与进度条指示器结合使用的消息。

 ![具有进度栏的状态栏](../../extensibility/ux-guidelines/media/0903-03_statusbarprogressbar.png "0903-03_StatusBarProgressBar")

 **具有进度栏的状态栏**

 ![具有消息传递的状态栏](../../extensibility/ux-guidelines/media/0903-04_statusbarmessage.png "0903-04_StatusBarMessage")

 **包含文本描述的状态栏**

##### <a name="infobar"></a>信息栏
 与状态栏类似，信息栏提供上下文通知和消息传递，也可以与不确定的进度指示器（如进度栏或微调器）配对。 信息栏不应提供粒度级别进度或确定进度指示。 请参阅[信息栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)。

 ![具有进度栏和消息传送的信息栏](../../extensibility/ux-guidelines/media/0903-05_infobar.png "0903-05_InfoBar")

 **包含进度栏和文本描述的信息栏**

 ![窗口中的信息栏](../../extensibility/ux-guidelines/media/0903-06_infobarinwindow.png "0903-06_InfoBarInWindow")

##### <a name="inline"></a>内联
 内联进度指示可以由任何进度加载程序类型表示。 通常，进度指示器与消息传递配对，但这不是要求。

 ![内联进度微调框](../../extensibility/ux-guidelines/media/0903-07_inlinespinner.png "0903-07_InlineSpinner")

 **微调器与文本描述相结合**

 ![内联堆积进度栏](../../extensibility/ux-guidelines/media/0903-08_inlinestackedprogress.png "0903-08_InlineStackedProgress")

 **确定堆叠进度条**

 ![内联进度消息传递](../../extensibility/ux-guidelines/media/0903-09_inlinetext.png "0903-09_InlineText")

 **服务器资源管理器内联文本：刷新...**

##### <a name="tool-windows"></a>工具窗口
 全局进度指示由位于工具栏正下方的不确定进度条表示。

 ![全局不确定的进度栏](../../extensibility/ux-guidelines/media/0903-23_globalindeterminate.png "0903-23_GlobalIndeterminate")

 **团队资源管理器全局不确定进度栏**

##### <a name="dialogs"></a>对话框
 对话框可以包含任何进度加载程序类型。 进度指示器可以与消息传递配对，并与多个级别的进度指示相结合，以表示粒度和子流程。

 ![具有多个进度指示器类型的对话框](../../extensibility/ux-guidelines/media/0903-11_dialog.png "0903-11_Dialog")

 **具有并发进程和多个进度指示器类型的可视化工作室对话框**

 ![具有进度加载器和消息传递的对话框](../../extensibility/ux-guidelines/media/0903-12_dialog2.png "0903-12_Dialog2")

 **带进度加载器和消息在线命令的可视化工作室对话框**

##### <a name="document-well"></a>文档良好
 文档井可以结合控件显示多个进度加载程序类型。

 ![文档井中的进度消息传递](../../extensibility/ux-guidelines/media/0903-13_documentwell.png "0903-13_DocumentWell")

 **工具栏下方不确定进度栏**

##### <a name="output-window"></a>输出窗口
 输出窗口适用于通过内联文本消息处理进程进度和持续进度状态。 您应该使用状态栏以及任何"输出"窗口进度报告。

 ![输出窗口中的进度消息传递](../../extensibility/ux-guidelines/media/0903-14_outputwindow.png "0903-14_OutputWindow")

 **输出窗口，具有正在进行的进程状态和等待消息**

## <a name="infobars"></a><a name="BKMK_Infobars"></a>信息栏

### <a name="overview"></a>概述
 信息栏为用户提供了接近其注意点的指示器，使用共享信息栏控件可确保视觉外观和交互的一致性。

 ![信息栏](../../extensibility/ux-guidelines/media/0904-01_infobar.png "0904-01_Infobar")

 **可视化工作室中的信息栏**

#### <a name="appropriate-uses-for-an-infobar"></a>信息栏的适当用途

- 为用户提供与当前上下文相关的非阻塞但重要的消息

- 指示 UI 处于具有某些交互影响的特定状态或条件，例如历史调试

- 通知用户系统检测到问题，例如当扩展导致性能问题时

- 为用户提供一种轻松执行操作的方法，例如当编辑器检测到文件具有混合选项卡和空格时

##### <a name="do"></a>请：

- 保持信息栏消息文本简短且指向点。

- 保持链接和按钮上的文本简洁。

- 确保提供给用户的"操作"选项最小，仅显示所需的操作。

##### <a name="dont"></a>不要：

- 使用信息栏提供应放置在工具栏中的标准命令。

- 使用信息栏代替模式对话框。

- 在窗口外创建浮动消息。

- 在同一窗口中的多个位置使用多个信息栏。

#### <a name="can-multiple-infobars-show-at-the-same-time"></a>多个信息栏可以同时显示吗？
 是，可以同时显示多个信息栏。 它们将以先到先得的顺序显示，第一个信息栏显示在顶部，下面显示其他信息栏。

 用户一次最多会看到三个信息栏，之后，如果有更多的信息栏可用，信息栏区域将变为可滚动。

### <a name="creating-an-infobar"></a>创建信息栏
 信息栏有四个部分，从左到右：

- **图标：** 这是要为信息栏添加任何图标的位置，例如警告图标。

- **文本：** 如果需要，可以添加文本来描述用户所处的方案/情况以及文本中的链接。 记住要保持文本简洁。

- **操作：** 此部分应包含用户可以在信息栏中执行的操作的链接和按钮。

- **关闭按钮：** 右侧的最后一个部分可以有一个关闭按钮。

#### <a name="creating-a-standard-infobar-in-managed-code"></a>在托管代码中创建标准信息栏
 InfoBarModel 类可用于为信息栏创建数据源。 使用以下四个构造函数之一：

```
public InfoBarModel(IEnumerable<IVsInfoBarTextSpan> textSpans, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);

```

```
public InfoBarModel(string text, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);

```

```
public InfoBarModel(IEnumerable<IVsInfoBarTextSpan> textSpans, IEnumerable<IVsInfoBarActionItem> actionItems, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);

```

```
public InfoBarModel(string text, IEnumerable<IVsInfoBarActionItem> actionItems, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);
```

 下面是一个示例，该示例创建一个信息栏模型，其中包含一些带有超链接、操作按钮和图标的文本。

 ![具有超链接的信息栏](../../extensibility/ux-guidelines/media/0904-02_infobarhyperlink.png "0904-02_InfobarHyperlink")

```
var infoBar = new InfoBarModel(
    textSpans: new[]
    {
        new InfoBarTextSpan("This is a "),
        new InfoBarHyperlink("hyperlink"),
        new InfoBarTextSpan(" InfoBar.")
    },
    actionItems: new[]
    {
        new InfoBarButton("Click Me")
    },
    image: KnownMonikers.StatusInformation,
    isCloseButtonVisible: true);

```

#### <a name="creating-a-standard-infobar-in-native-code"></a>在本机代码中创建标准信息栏
 实现 IVsInfoBar 接口，以便提供来自本机代码的信息栏。

```
public interface IVsInfoBar
{
    IVsInfoBarActionItemCollection ActionItems { get; }
    ImageMoniker Image { get; }
    bool IsCloseButtonVisible { get; }
    IVsInfoBarTextSpanCollection TextSpans { get; }
}

```

#### <a name="getting-an-infobar-uielement-from-an-infobar"></a>从信息栏获取信息栏 UIElement
 InfoBarModel 或 IVsInfoBar 实现是数据模型，必须转换为 UIElement 才能显示在 UI 中。 可以使用 SVInfoBarUIFactory/IVsInfoBarUIFactory 服务检索 UIElement。

```
private bool TryCreateInfoBarUI(IVsInfoBar infoBar, out IVsInfoBarUIElement uiElement)
{
    IVsInfoBarUIFactory infoBarUIFactory = serviceProvider.GetService(typeof(SVsInfoBarUIFactory)) as IVsInfoBarUIFactory;
    if (infoBarUIFactory == null)
    {
        uiElement = null;
        return false;
    }

    uiElement = infoBarUIFactory.CreateInfoBar(infoBar);
    return uiElement != null;
}
```

### <a name="placement"></a>位置
 信息栏可以在以下一个或多个位置显示：

- 工具窗口

- 在文档选项卡中

> [!IMPORTANT]
> 可以定位信息栏来提供有关全局上下文的消息。 这将显示在工具栏和文档之间。 不建议这样做，因为它会导致 IDE 的"跳跃和抖动"问题，除非绝对必要和适当，否则应避免这样做。

#### <a name="placing-an-infobar-in-a-toolwindowpane"></a>在工具窗口窗格中放置信息栏
 工具窗口窗格.AddInfoBar（IVsInfoBar）方法可用于向工具窗口添加信息栏。 此 API 可以添加 IVsInfoBar（其中 InfoBarModel 是默认实现）或 IVsUI元素。

#### <a name="placing-an-infobar-in-a-document-or-non-toolwindowpane"></a>在文档或非工具窗口窗格中放置信息栏
 要将信息栏放置在任何 IVWindowFrame 中，请使用VSFPROPID_InfoBarHost属性获取框架的 IVsInfoBarHost，然后添加信息栏 UIElement。

```
private void AddInfoBar(IVsWindowFrame frame, IVsUIElement uiElement)
{
    IVsInfoBarHost infoBarHost;
    if (TryGetInfoBarHost(frame, out infoBarHost))
    {
        infoBarHost.AddInfoBar(uiElement);
    }
}
private bool TryGetInfoBarHost(IVsWindowFrame frame, out IVsInfoBarHost infoBarHost)
{
    object infoBarHostObj;
    if (ErrorHandler.Failed(frame.GetProperty((int)__VSFPROPID7.VSFPROPID_InfoBarHost, out infoBarHostObj)))
    {
        infoBarHost = null;
        return false;
    }

    infoBarHost = infoBarHostObj as IVsInfoBarHost;
    return infoBarHost != null;
}

```

#### <a name="placing-an-infobar-in-the-main-window"></a>在主窗口中放置信息栏
 要在主窗口中放置信息栏，请使用 IVsShell 服务VSSPROPID_MainWindowInfoBarHost获取主窗口的 IVsInfoBarHost，然后将信息栏 UIElement 添加到其中。

### <a name="will-i-know-when-the-user-takes-action-in-my-infobar"></a>我是否会知道用户何时在我的信息栏中执行操作？
 是的，我们将将每个事件操作返回给信息栏作者。 然后，信息栏作者根据信息栏中的用户选择在 IDE 中执行操作。 信息栏将自动从单击其"关闭"按钮的主机中删除，但如果关闭后需要删除其他信息栏，则需要执行其他工作。 遥测还需要由每个信息栏独立记录。

#### <a name="receiving-infobar-events-in-a-toolwindowpane"></a>在工具窗口窗格中接收信息栏事件
 工具窗口窗格有两个用于信息栏的事件。 关闭工具窗口窗格中的信息栏时，将引发信息栏关闭事件。 单击信息栏内的超链接或按钮时，将引发信息栏项目单击事件。

#### <a name="receiving-infobar-events-directly-from-the-uielement"></a>直接从 UIElement 接收信息栏事件
 IVsInfoBarUIElement.建议可用于直接从信息栏的 UIElement 订阅事件。 实施 IVsInfoBarUI 事件将允许作者接收关闭和单击事件。

```
public interface IVsInfoBarUIEvents
{
    void OnActionItemClicked(IVsInfoBarUIElement infoBarUIElement, IVsInfoBarActionItem actionItem);
    void OnClosed(IVsInfoBarUIElement infoBarUIElement);
}

```

## <a name="error-validation"></a><a name="BKMK_ErrorValidation"></a>错误验证
 当用户输入不可接受的信息时（例如跳过所需字段或以不正确的格式输入数据时）时，最好在控件附近使用控制验证或反馈，而不是使用阻塞弹出错误对话框。

### <a name="field-validation"></a>字段验证
 窗体和字段验证由三个组件组成：控件、图标和工具提示。 虽然可以使用多种类型的控件，但文本框将用作示例。

 ![字段验证&#40;空白&#41;](../../extensibility/ux-guidelines/media/0905-01_fieldvalidation.png "0905-01_FieldValidation")

 如果需要该字段，则应该有水印文本，说明**\<所需的>，** 字段背景应为浅黄色 （VSColor： `Environment.ControlEditRequiredBackground`）， 前景应为灰色 （VSColor： `Environment.ControlEditRequiredHintText`）：

 ![具有“必须”标签的字段验证](../../extensibility/ux-guidelines/media/0905-02_fieldvalidationrequired.png "0905-02_FieldValidationRequired")

 程序可以确定控件处于在焦点移动到其他控件时或当用户单击 [OK] 提交按钮或当用户保存文档或表单时*输入的无效内容*的状态。

 确定无效内容状态后，控件内或位于控件旁边会出现一个图标。 描述错误的工具提示应出现在图标或控件的悬停上。 此外，在创建无效状态的控件周围应显示 1 像素边框。

 ![字段验证布局规范](../../extensibility/ux-guidelines/media/0905-03_layoutspecs.png "0905-03_LayoutSpecs")

 **现场验证的布局规范**

#### <a name="acceptable-variations-for-icon-location"></a>图标位置的可接受变体
 在无数独特的情况下，用户需要了解验证错误。 考虑 UI 的控制类型和配置，选择适合您的情况的图标位置。

 ![图标位置的可接受位置](../../extensibility/ux-guidelines/media/0905-04_iconlocation.png "0905-04_IconLocation")

 **字段验证图标位置的可接受变体**

#### <a name="validation-requiring-a-round-trip-to-a-server-or-network-connection"></a>需要往返服务器或网络连接的验证
 在某些情况下，需要往返服务器来验证内容，显示用户进度、已验证和错误状态非常重要。 下图显示了此案例的示例和建议的 UI。

 ![涉及到服务器的往返行程的验证](../../extensibility/ux-guidelines/media/0905-05_roundtrip.png "0905-05_RoundTrip")

 **涉及到服务器的往返行程的验证**

 请注意，必须提供足够的可用空间，以容纳"验证..."和"重试"文本。

#### <a name="in-place-warning-text"></a>就地警告文本
 当有空间将错误消息置于错误状态时，最好仅使用工具提示。

 ![在&#45;位置警告](../../extensibility/ux-guidelines/media/0905-06_inplacewarning.png "0905-06_InPlaceWarning")

 **就地警告文本**

#### <a name="watermarks"></a>水印
 有时，整个控件或窗口处于错误状态。 在此情况下，使用水印指示错误。

 ![水印](../../extensibility/ux-guidelines/media/0905-07_watermark.png "0905-07_Watermark")

 **水印字段验证**
