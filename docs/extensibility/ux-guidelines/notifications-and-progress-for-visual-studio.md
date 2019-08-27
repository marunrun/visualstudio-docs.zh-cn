---
title: Visual Studio 的通知和进度 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f0ef65e9-0f1f-45f4-9f25-6e2398691168
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c5ca3f02c37a76e31ad76f6875110487dffefd49
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310889"
---
# <a name="notifications-and-progress-for-visual-studio"></a>Visual Studio 的通知和进度
## <a name="BKMK_NotificationSystems"></a> 通知系统

### <a name="overview"></a>概述
 有几种方法来通知用户在 Visual Studio 中有关其软件开发任务发生。

 当实现任何种类的通知：

- **保持为最小值通知数**有效数字。 通知消息应适用于大多数 Visual Studio 用户或特定功能区域的用户。 过多使用通知可能 sidetrack 用户还是不感知的易于使用的系统。

- **请确保您要呈现清晰、 可操作邮件**用户可用来调用相应的上下文进行更复杂的选择和采取进一步操作。

- **相应地提供同步和异步消息。** 同步通知指示出现需要直接处理，例如何时发生故障的 web 服务或代码引发异常。 在模式对话框中，如要求其输入的方式立即在这些情况下，应通知用户。 异步通知是一种是用户应该了解，但不是会要求起作用时立即，如生成操作完成时或网站部署完成。 这些消息应更环境并不会中断用户的任务流。

- **使用模式对话框仅在需要以防止用户采取进一步操作时**之前确认消息或在做出决定在对话框中显示。

- **删除环境的通知时它们将不再有效。** 不需要用户若要消除通知，如果它们已采取措施来解决的问题的通知。

- **请注意，通知可能导致错误关联。** 用户可能会认为，一个或多个其操作触发通知时实际上没有任何因果关系。 清除为上下文、 触发器和通知的源通知消息。

### <a name="choosing-the-right-method"></a>选择正确的方法
 使用此表来帮助你选择正确的方法以通知用户您的消息。

|方法|使用|不使用|
|------------|---------|----------------|
|[模式错误消息对话框](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ModalErrorMessageDialogs)|在继续之前需要用户响应时使用。|不要使用无需阻止用户和中断其流时。 避免使用模式对话框，它是否可以在另一个、 少受侵入的方式显示消息。|
|[IDE 状态栏会显示](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_IDEStatusBar)|有关状态的进程的环境文本的信息时使用。|不单独使用。 最适合与一起使用另一种反馈机制。|
|[嵌入式信息栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedInfobar)|在工具窗口或文档窗口中，使用通知进度、 错误状态、 结果，和/或可操作的信息。|不要使用如果信息不是放置该信息栏的位置相关。<br /><br /> 不要使用文档/工具窗口外。|
|[鼠标光标会更改](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_MouseCursorChanges)|可能用于通知进程怎么回事。 此外用于通知有状态更改鼠标，如鼠标光标拖放时进度或处于某种模式，如绘制模式。|请不要用于短进度更改或 fluttering 的光标是否可能 （例如，当取决于正在运行过程耗时较长而不是为整个过程的部分）。|
|[进度指示器](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotSysProgressIndicators)|当你需要报告进度 （确定或不确定） 时使用。 有各种进度指示器类型和每个特定的使用。 请参阅[进度指示器](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators)。||
|[Visual Studio 通知窗口](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_VSNotificationsToolWindow)|通知窗口不能公开扩展。 但是，它用于进行通信的一系列有关 Visual Studio 中，包括与您的许可证和更新到 Visual Studio 或包的信息性通知的关键问题的消息。|不要使用为其他类型的通知。|
|[错误列表](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ErrorList)|当问题直接与用户的当前打开的解决方案时遇到问题 （错误/警告/信息） 时，他们可能需要对代码执行操作。<br /><br /> 这将包括，例如：<br /><br /> 编译器消息 （错误/警告/信息）<br /><br /> 的有关代码代码分析器/诊断消息<br /><br /> -生成的消息<br /><br /> 可能是适用于项目或解决方案文件中，相关的问题，但首先考虑的解决方案资源管理器指示。|不要使用不具有与用户的打开的解决方案代码的任何关系的项。|
|编辑器通知：灯泡|已修复，可用于修补在打开的文件中存在的问题时使用。<br /><br /> 请注意灯泡还应使用用于托管按需、 重构，例如用户的代码执行但在这种情况下不会出现"通知 style。"快速操作|不要使用打开的文件没有任何关系的项。|
|编辑器通知：波形曲线|使用其打开的代码 （例如，红色波浪线有错误） 的特定范围的问题向用户发出警报。|为向特定范围的打开的代码不相关的项不使用。|
|[嵌入式的状态栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedStatusBars)|用于提供与相关的内容或上下文特定的工具窗口、 文档窗口或对话框窗口中的进程的状态。|请不要用于常规产品通知、 进程或特定时段内没有任何关系的内容的项。|
|[Windows 任务栏通知](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_WindowsTray)|用于呈现进程外的进程的通知或伴生应用程序。|请不要用于与 IDE 相关的通知。|
|[通知气泡](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotificationBubbles)|使用远程过程的通知或更改**外部**的 IDE。|请不要用于作为一种方式通知用户的进程**内**IDE。|

### <a name="notification-methods"></a>通知方法

#### <a name="BKMK_ModalErrorMessageDialogs"></a> 模式错误消息对话框
 模式错误消息对话框用于显示错误消息，要求用户确认或操作。

 ![模式错误消息](../../extensibility/ux-guidelines/media/0901-01_modalerrormessage.png "0901年 01_ModalErrorMessage")

 **模式错误消息对话框提醒用户数据库无效的连接字符串**

#### <a name="BKMK_IDEStatusBar"></a> IDE 状态栏会显示
 可能性用户注意到状态栏文本关联到其全能计算机体验和 Windows 平台上特定的经验。 Visual Studio 客户群往往是这两个方面经验丰富，但即使知识渊博的 Windows 用户可能会缺失状态栏中的更改。 因此，状态栏，最好使用用于提供信息或作为冗余提示信息的信息显示在其他位置。 在对话框中，或通知工具窗口中，应提供任何类型的用户必须立即解决的关键信息。

 Visual Studio 状态栏旨在允许多种类型的信息，以显示。 它分为反馈、 设计器中，进度条、 动画和客户端的区域。

 反馈区域和设计器区域始终是可见的。 进度栏，动画区域始终是动态的、 基于用户上下文。 设计器区域具有静态宽度由从短信的附带资源提取字符串的长度。 这样，本地化来调整宽度大小而无需在代码更改。 为英语，此字符串的宽度为大约 220 像素。 设计器区域将能够正常工作，反馈区域将 absorb 剩余的空间。

 状态栏还着色通信各种 IDE 状态更改，例如当 IDE 处于调试模式下添加视觉效果和功能的值。

 ![IDE 状态栏颜色更改](../../extensibility/ux-guidelines/media/0901-02_idestatusbar.png "0901年 02_IDEStatusBar")

 **IDE 状态栏颜色**

#### <a name="BKMK_EmbeddedInfobar"></a> 嵌入式信息栏
 信息栏可在文档窗口或工具窗口顶部的通知状态或条件的用户。 它还可以提供命令，以便用户可以轻松地执行操作的方法。 信息栏是一个标准 shell 控件。 避免创建你自己，以执行操作，并显示在 IDE 中与其他人不一致。 请参阅[信息栏时](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)有关实现的详细信息和使用指南。

 ![嵌入式信息栏](../../extensibility/ux-guidelines/media/0901-03_embeddedinfobar.png "0901年 03_EmbeddedInfobar")

 **信息栏嵌入在文档窗口中，警报 IDE 处于历史调试模式下，编辑器将不会响应相同的方式与在标准调试模式下的用户。**

#### <a name="BKMK_MouseCursorChanges"></a> 鼠标光标会更改
 更改时鼠标光标，请使用与 VSColor 服务并且已与游标相关联的颜色。 光标发生变化，可用于指示正在进行的操作，以及命中的区域用户悬停的目标，可以拖动、 放置到上，或用来选择某一对象的位置。

 仅当所有可用的 CPU 时间必须保留操作，防止用户表达任何进一步的输入时，请使用忙/等待鼠标光标。 与编写良好的应用程序使用多线程处理大多数情况下，当阻止用户执行其他操作的时间应该很少见。

 请注意光标发生变化，非常有用，因为一个冗余信息提示显示其他位置。 不要依赖于光标更改为至关重要，用户必须解决尝试传达的内容时尤其是与用户进行通信的唯一方式。

#### <a name="BKMK_NotSysProgressIndicators"></a> 进度指示器
 进度指示器向用户反馈提供在需要超过几秒钟来完成的过程至关重要。 可以显示进度指示器的就地 （附近操作正在进行中的启动点），嵌入的状态栏中、 在模式对话框中，或在 Visual Studio 状态栏中。 遵循中的指导[进度指示器](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators)有关其使用和实现。

#### <a name="BKMK_VSNotificationsToolWindow"></a> Visual Studio 通知窗口
 Visual Studio 通知窗口将通知有关许可、 环境 (Visual Studio)、 扩展和更新的开发人员。 用户可以关闭单个通知，或者可以选择忽略某些类型的通知。 在中管理忽略通知的列表**工具 > 选项**页。

 通知窗口不是当前可扩展的。

 ![Visual Studio 通知窗口](../../extensibility/ux-guidelines/media/0901-06_vsnotificationswindow.png "0901年 06_VSNotificationsWindow")

 **Visual Studio 通知工具窗口**

#### <a name="BKMK_ErrorList"></a> 错误列表
 错误列表中的通知指示错误和警告的编译过程中发生和或生成过程中，并允许用户导航到该特定的代码错误的代码中。

 ![错误列表](../../extensibility/ux-guidelines/media/0901-08_errorlist.png "0901年 08_ErrorList")

 **在 Visual Studio 中的错误列表**

#### <a name="BKMK_EmbeddedStatusBars"></a> 嵌入式的状态栏
 IDE 状态栏是动态的使用其客户端区域上下文设置为活动文档窗口和更新用户的上下文和/或系统响应上的信息，因为很难维护连续显示的信息或提供长期的状态异步进程。 例如，IDE 状态栏会显示不适合的多个运行和/或立即可操作的项选择的测试运行结果的通知。 请务必保留此类上下文中的文档或工具窗口进行了选择用户或将启动一个进程的状态信息。

 ![Embedded status bar](../../extensibility/ux-guidelines/media/0901-09_embeddedstatusbar.png "0901-09_EmbeddedStatusBar")

 **在 Visual Studio 中的嵌入式的状态栏**

#### <a name="BKMK_WindowsTray"></a> Windows 任务栏通知
 Windows 任务栏上的 Windows 通知区域位于旁边系统时钟。 很多实用程序和软件组件提供此区域中的图标，以便用户可以获取用于系统级任务，如更改屏幕分辨率或获取软件更新的上下文菜单。

 环境级别通知应该显示在 Visual Studio 通知中心，不在 Windows 通知区域中。

#### <a name="BKMK_NotificationBubbles"></a> 通知气泡
 通知气泡可为信息性消息编辑器/设计器中或在 Windows 通知区域的一部分出现。 用户感觉这是一项权益的非关键通知这些气泡为更高版本，它们可以解决的问题。 不适合于用户必须立即解决的关键信息气泡。 如果您在 Visual Studio 中使用通知气泡，请按照[通知气泡的 Windows 桌面指南](/windows/desktop/uxguide/mess-notif)。

 ![通知气泡](../../extensibility/ux-guidelines/media/0901-07_notificationbubbles.png "0901年 07_NotificationBubbles")

 **用于 Visual Studio 的 Windows 通知区域中的通知气泡**

## <a name="BKMK_ProgressIndicators"></a> 进度指示器

### <a name="overview"></a>概述
 进度指示器会为用户提供反馈的通知系统的一个重要部分。 进程和操作将完成时，他们会告诉用户。 熟悉的指示器类型包括进度条、 旋转游标和动态的图标。 类型和进度指示器的位置取决于完成所需的上下文，包括报告的内容和多长时间的进程或操作。

#### <a name="factors"></a>因素
 若要确定哪种指示器类型适合，您需要确定以下因素。

1. **计时：** 操作所花的时间长度

2. **模式：** 操作是模式适合环境 （锁定 UI 过程完成之前）

3. **永久/暂时的：** 是否需要在更高版本时进行报告和/或可查看正在进行的最终结果

4. **确定/不确定：** 可以计算操作结束时间和进度

5. **图/Textual 位置：** 进度或进程是否在一条消息或一个特定的控件，例如树控件的主体中捕获的内联

6. **邻近：** 进度应位于较近的 UI 与相关的。 （例如，可以在状态栏中可能是距离遥远，或没有要启动进程的按钮附近？）

#### <a name="determinate-progress"></a>确定的进度

|进度类型|何时以及如何使用|说明|
|-------------------|-------------------------|-----------|
|进度栏 （确定）|预期的持续时间 > 5 秒。<br /><br /> 可能包括进程详细信息的文本的说明。|**不**将文本嵌入到动画。|
|信息栏|与上下文 UI 相关联的消息传递。 请参阅[信息栏时](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)。<br /><br /> 可能包括进程详细信息的文本的说明。|**不**需要来指定多个进程时使用多个信息栏。 改为使用堆积的进度栏。|
|输出窗口|暂时性的通知： 该用户希望应用程序级过程**查看**完成后的详细信息。|**不**如果用户将需要更高版本引用的数据，请使用。|
|日志文件|与在情况下 intransient 通知配合使用时务必**保存**完成后的详细信息。||
|状态栏|暂时性的通知： 该用户将应用程序级过程**不需要**完成后的详细信息。<br /><br /> 包括嵌入的进度栏。<br /><br /> 可能包括进程详细信息的文本的说明。||

#### <a name="indeterminate-progress"></a>不确定的进度

|进度类型|何时以及如何使用|说明|
|-------------------|-------------------------|-----------|
|（不确定） 的进度栏|预期的持续时间 > 5 秒。<br /><br /> 可能包括进程详细信息的文本的说明。|**不**将文本嵌入到动画。|
|Ants （经过动画处理的水平点）|往返到服务器。<br /><br /> 放置在父容器的顶部上下文的 near 点。|**不**如果没有父级的整个容器，请使用。|
|微调控件 （进度环）|关联上下文用户界面时，或其中的空间是一个考虑因素的进程。<br /><br /> 可能包括进程详细信息的文本的说明。||
|信息栏|与上下文 UI 相关联的消息传递。 请参阅[信息栏时](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)。|**不**需要来指定多个进程时使用多个信息栏。 改为使用堆积的进度栏。|
|输出窗口|暂时性的通知： 该用户将希望应用程序级过程**查看**完成后的详细信息。|**不**用于需要在会话之间持久保存的信息。|
|日志文件|与在情况下 intransient 通知配合使用时务必**保存**完成后的详细信息。||
|状态栏|暂时性的通知： 该用户将应用程序级过程**不需要**完成后的详细信息。<br /><br /> 包括嵌入的进度栏。<br /><br /> 可能包括进程详细信息的文本的说明。||

### <a name="progress-indicator-types"></a>进度指示器类型

#### <a name="progress-bars"></a>进度栏

##### <a name="indeterminate"></a>不确定
 ![不确定的进度栏](../../extensibility/ux-guidelines/media/0901-04_indeterminate.png "0901年 04_Indeterminate")

 **不确定的进度栏**

 "不确定"表示操作的总体进度或不能确定过程。 对于需要一段时间的不受限制的操作中使用不确定的进度条，或访问的对象数未知。 使用的文本说明伴随发生了什么情况。 使用超时为边界提供对基于时间的操作。 不确定的进度条使用动画来显示进度操作正在进行，但不提供任何其他信息。 不要选择仅根据单独的准确性可能缺少一个不确定的进度栏。

##### <a name="determinate"></a>确定
 ![确定的进度栏](../../extensibility/ux-guidelines/media/0901-05_determinate.png "0901年 05_Determinate")

 **确定的进度栏**

 "确定"意味着与操作或处理需要有限的数量的时间，即使这段时间不能准确预测。 清楚地表示完成。 不要让一个进度栏，请转到 100%，除非该操作已完成。 确定的进度栏动画将从左到右从 0 到 100%。

 永远不会移动操作期间向后的进度指示器。 栏应向前移动稳定时该操作开始和结束时达到 100%。 进度栏的要点是使用户了解整个操作需要花多长，而不考虑所涉及的步骤数。

##### <a name="concurrent-reporting-stacked-progress-bars"></a>并发报告 （堆积的进度栏）
 如果操作将需要较长的时间-可能是可能使用多个分钟-然后两个进度栏，其中一个，显示总体进度的操作，另一个用于当前步骤的进度。 例如，如果安装程序正在复制多个文件，然后一个进度栏可用于指示多长时间的整个过程需要的时间，第二个可以指示当前文件的百分比，或者复制目录。 不超过五个并发操作或使用堆积的进度栏的进程报告。 如果有五个并发操作或报表的进程，使用一个模式对话框与取消按钮以及报表进度详细信息到输出窗口。

##### <a name="textual-descriptions"></a>文字说明
 使用随附发生了什么情况的文本说明和估计的完成时间。 如果无法确定操作需要多长时间，用于提供反馈更好的选择可能的动画的图标而不是一个进度栏。

 Visual Studio 提供可由任何产品集成到 Visual Studio 的状态栏中的一个标准进度栏。 有关所发生的情况时的动画进度栏的文本说明，可以更新状态栏文本。

#### <a name="other-progress-indicators"></a>其他进度指示器

##### <a name="ants-animated-horizontal-dots"></a>Ants （经过动画处理的水平点）
 ![进度 ants](../../extensibility/ux-guidelines/media/0903-01_ants.png "0903年 01_Ants")

 "蚂蚁"经过动画处理的水平点、 不确定的往返服务器进程提供的视觉参考。

##### <a name="spinner-progress-ring"></a>微调控件 （进度环）
 ![进度微调框](../../extensibility/ux-guidelines/media/0903-02_spinner.png "0903年 02_Spinner")

 微调框 （也称为"进度环"） 是不确定的进度指示器主要用于相对于上下文的 UI。 在紧靠其相关内容，例如文本类别标题、 消息传递，或控件中显示微调控件。

##### <a name="cursor-feedback"></a>游标的反馈
 对于需要 2 到 7 秒钟的操作，提供游标反馈。 通常情况下，这意味着使用操作系统提供的将等待光标。 有关指南，请参阅 MSDN 文章[Cursors.Wait 属性](/dotnet/api/system.windows.input.cursors.wait)。

#### <a name="progress-indicator-locations"></a>进度指示器位置

##### <a name="status-bar"></a>状态栏
 状态栏为你的应用程序提供了一个位置来向用户显示消息和有用的信息而不会中断用户的工作。 通常显示在窗口的底部，进度的状态将与一个进度栏指示符结合使用包括有关进度的度量值的消息的工具提示窗格。

 ![具有进度栏的状态栏](../../extensibility/ux-guidelines/media/0903-03_statusbarprogressbar.png "0903年 03_StatusBarProgressBar")

 **具有进度栏的状态栏**

 ![状态栏使用消息传送](../../extensibility/ux-guidelines/media/0903-04_statusbarmessage.png "0903年 04_StatusBarMessage")

 **具有文本说明的状态栏**

##### <a name="infobar"></a>信息栏
 类似于状态栏，信息栏提供上下文的通知和消息传送，这还可以使用不确定的进度指示器，如进度栏或微调配对。 信息栏不应提供精细的级别进度或确定的进度指示。 请参阅[信息栏时](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)。

 ![具有进度栏和消息传送的信息栏](../../extensibility/ux-guidelines/media/0903-05_infobar.png "0903年 05_InfoBar")

 **具有进度栏和文本说明的信息栏**

 ![一个窗口中的信息栏](../../extensibility/ux-guidelines/media/0903-06_infobarinwindow.png "0903年 06_InfoBarInWindow")

##### <a name="inline"></a>内联
 内联进度指示可表示任何进度加载器类型。 通常使用消息传送，配对的进度指示器，但这不是一项要求。

 ![内联进度微调框](../../extensibility/ux-guidelines/media/0903-07_inlinespinner.png "0903年 07_InlineSpinner")

 **微调框与文本说明结合使用**

 ![内联堆积进度栏](../../extensibility/ux-guidelines/media/0903-08_inlinestackedprogress.png "0903年 08_InlineStackedProgress")

 **确定的堆积的进度条**

 ![内联进度消息传递](../../extensibility/ux-guidelines/media/0903-09_inlinetext.png "0903年 09_InlineText")

 **服务器资源管理器中内联文本：正在刷新...**

##### <a name="tool-windows"></a>工具窗口
 由正下方的工具栏中定位的不确定的进度栏表示全局进度指示。

 ![全局不确定的进度栏](../../extensibility/ux-guidelines/media/0903-23_globalindeterminate.png "0903年 23_GlobalIndeterminate")

 **团队资源管理器全局不确定的进度栏**

##### <a name="dialogs"></a>对话框
 对话框可以包含任何进度加载器类型。 进度指示器可以是与消息传送成对出现，以及结合多个级别的精细的表示和子进程的进度指示。

 ![具有多个进度指示器类型的对话框](../../extensibility/ux-guidelines/media/0903-11_dialog.png "0903年 11_Dialog")

 **Visual Studio 对话框，使用并发进程数和多个进度指示器类型**

 ![具有进度加载器和消息传送的对话框](../../extensibility/ux-guidelines/media/0903-12_dialog2.png "0903年 12_Dialog2")

 **具有进度加载器和消息传送内联命令的 visual Studio 对话框**

##### <a name="document-well"></a>文档井中
 嗯，文档可以与控件结合使用显示多个进度加载器类型。

 ![进度消息传递文档中也](../../extensibility/ux-guidelines/media/0903-13_documentwell.png "0903年 13_DocumentWell")

 **不确定的进度栏下方工具栏**

##### <a name="output-window"></a>输出窗口
 输出窗口是合适的处理过程前进和通过内联文本消息传送的正在进行的进度状态。 应使用状态栏以及任何输出窗口进度报告。

 ![正在进行中输出窗口的消息传送](../../extensibility/ux-guidelines/media/0903-14_outputwindow.png "0903年 14_OutputWindow")

 **正在进行的进程的状态下的输出窗口和等待消息传送**

## <a name="BKMK_Infobars"></a> 信息栏

### <a name="overview"></a>概述
 信息栏时为用户提供的关注其点接近指示器，并使用共享的信息栏控件确保视觉外观和交互的一致性。

 ![Infobar](../../extensibility/ux-guidelines/media/0904-01_infobar.png "0904-01_Infobar")

 **在 Visual Studio 中的信息栏**

#### <a name="appropriate-uses-for-an-infobar"></a>正确使用信息栏

- 若要为用户提供与当前上下文相关的非阻塞的但很重要消息

- 以指示在 UI 中的某个状态或条件执行的某些交互的含义，如历史调试

- 若要通知用户系统已检测到问题，例如当某个扩展导致性能问题

- 提供一种方法来轻松地执行操作，例如当编辑器中检测到一个文件具有混合制表符和空格的用户

##### <a name="do"></a>执行操作：

- 简单地说，到点，请保留信息栏消息文本。

- 保持简洁上链接和按钮的文本。

- 请确保你为用户提供的"操作"选项非常小，显示所需的操作。

##### <a name="dont"></a>不要：

- 信息栏用于提供应放置在工具栏中的标准命令。

- 使用信息栏来代替一个模式对话框。

- 创建的时段之外的浮点型消息。

- 在同一个窗口中的多个位置中使用多个信息栏。

#### <a name="can-multiple-infobars-show-at-the-same-time"></a>可以同时显示多个信息栏？
 是的多个信息栏时可以显示在同一时间。 使用 top 和其他信息栏显示下面显示的第一个信息栏，将第一个先来先服务顺序显示它们。

 用户将看到一次最多三个信息栏时后，如果多个信息栏时可供使用，信息栏区域将变得可滚动。

### <a name="creating-an-infobar"></a>创建一个信息栏
 信息栏包含四个部分，从左到右：

- **图标：** 这是将在其中添加任何图标你想要显示的信息栏，如警告图标。

- **文本：** 如果需要，可以添加文本以描述方案/情况用户是在中，以及文本内的链接。 请记住保持简洁的文本。

- **操作：** 本部分应包含一些链接和按钮，用户可以在你的信息栏中执行的操作。

- **关闭按钮：** 向右的最后一个部分可以有一个关闭按钮。

#### <a name="creating-a-standard-infobar-in-managed-code"></a>在托管代码中创建标准的信息栏
 InfoBarModel 类可用于创建一个信息栏的数据源。 使用以下四个构造函数之一：

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

 下面是示例用于创建 InfoBarModel 包含一些文本与超链接、 一个操作按钮和图标。

 ![具有超链接的信息栏](../../extensibility/ux-guidelines/media/0904-02_infobarhyperlink.png "0904年 02_InfobarHyperlink")

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

#### <a name="creating-a-standard-infobar-in-native-code"></a>在本机代码中创建标准的信息栏
 为了提供从本机代码的信息栏实现 IVsInfoBar 接口。

```
public interface IVsInfoBar
{
    IVsInfoBarActionItemCollection ActionItems { get; }
    ImageMoniker Image { get; }
    bool IsCloseButtonVisible { get; }
    IVsInfoBarTextSpanCollection TextSpans { get; }
}

```

#### <a name="getting-an-infobar-uielement-from-an-infobar"></a>信息栏 UIElement 获得一个信息栏
 InfoBarModel 或 IVsInfoBar 实现都必须打开 UIElement 到要在 UI 中显示的数据模型。 可通过 SVsInfoBarUIFactory/IVsInfoBarUIFactory 服务检索 UIElement。

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

### <a name="placement"></a>放置
 信息栏时可以在一个或多个以下位置中所示：

- 工具窗口

- 在文档选项卡

> [!IMPORTANT]
> 就可以放置一个信息栏，以提供有关全局上下文的消息。 这将显示工具栏和文档井中之间。 不建议，因为它会导致问题的"跳转和跃度"的 IDE，应当避免，除非绝对必要且适用。

#### <a name="placing-an-infobar-in-a-toolwindowpane"></a>置于 ToolWindowPane 信息栏
 ToolWindowPane.AddInfoBar(IVsInfoBar) 方法可以用于将一个信息栏添加到工具窗口。 此 API 可以添加 IVsInfoBar （哪个 InfoBarModel 为默认实现），或 ivsuielement。

#### <a name="placing-an-infobar-in-a-document-or-non-toolwindowpane"></a>在文档或非 ToolWindowPane 中放置一个信息栏
 要放入任何 IVsWindowFrame 信息栏，VSFPROPID_InfoBarHost 属性用于获取 IVsInfoBarHost 框架，以及如何将该信息栏 UIElement。

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

#### <a name="placing-an-infobar-in-the-main-window"></a>在主窗口中放置一个信息栏
 若要在主窗口中放置一个信息栏，IVsShell 服务 VSSPROPID_MainWindowInfoBarHost 用于获得主窗口 IVsInfoBarHost，然后向其中添加信息栏 UIElement。

### <a name="will-i-know-when-the-user-takes-action-in-my-infobar"></a>我知道如果用户在我的信息栏中执行的操作？
 是的我们将向信息栏作者返回每个事件的操作。 这样，它将最多信息栏作者可以基于该信息栏中的用户选择在 IDE 中执行操作。 信息栏时将自动从主机中删除其关闭按钮被单击，但如果其他信息栏时需要删除后关闭，则需要额外的工作。 遥测还将需要单独记录的每个信息栏。

#### <a name="receiving-infobar-events-in-a-toolwindowpane"></a>ToolWindowPane 中接收信息栏事件
 ToolWindowPane 具有两个事件的信息栏。 关闭信息栏中 ToolWindowPane 时引发 InfoBarClosed 事件。 单击超链接或按钮在信息栏时，将引发 InfoBarActionItemClicked 事件。

#### <a name="receiving-infobar-events-directly-from-the-uielement"></a>直接从 UIElement 接收信息栏事件
 IVsInfoBarUIElement.Advise 可以用于直接从一个信息栏 UIElement 订阅事件。 实现 IVsInfoBarUIEvents 将允许作者以关闭接收并单击事件。

```
public interface IVsInfoBarUIEvents
{
    void OnActionItemClicked(IVsInfoBarUIElement infoBarUIElement, IVsInfoBarActionItem actionItem);
    void OnClosed(IVsInfoBarUIElement infoBarUIElement);
}

```

## <a name="BKMK_ErrorValidation"></a> 错误验证
 当用户输入是不可接受的例如必填的字段时将跳过或格式不正确的数据输入的信息时，最好是使用控件验证或而不是使用阻止的弹出窗口错误对话框控件附近的反馈。

### <a name="field-validation"></a>字段验证
 窗体和字段验证三个组件组成： 一个控件、 一个图标和工具提示。 虽然多个类型的控件可以使用这，文本框中将用作示例。

 ![字段验证&#40;空白&#41;](../../extensibility/ux-guidelines/media/0905-01_fieldvalidation.png "0905年 01_FieldValidation")

 如果该字段是必需的则应有水印文本指出 **\<必需>** 字段背景颜色应光和黄色 (VSColor: `Environment.ControlEditRequiredBackground`) 和前台应为灰色 (VSColor: `Environment.ControlEditRequiredHintText`):

 ![字段"Required"标签的验证](../../extensibility/ux-guidelines/media/0905-02_fieldvalidationrequired.png "0905年 02_FieldValidationRequired")

 该程序可以确定控件是否处于的状态*输入的无效内容*焦点移动到另一个控件时或当用户单击确定提交按钮时或当用户保存文档或窗体。

 确定是无效的内容状态，在控件内或只是其旁边会出现一个图标。 描述错误的工具提示应显示的图标或控件的悬停时的。 此外，应创建状态无效控件周围显示 1 像素的边框。

 ![字段验证布局规范](../../extensibility/ux-guidelines/media/0905-03_layoutspecs.png "0905年 03_LayoutSpecs")

 **字段验证布局规范**

#### <a name="acceptable-variations-for-icon-location"></a>可接受的变体图标位置
 有大量用户需要了解验证错误的唯一情况。 考虑到的控件类型和配置在 UI 中，选择适合于您的具体情况的图标位置。

 ![图标位置的可接受位置](../../extensibility/ux-guidelines/media/0905-04_iconlocation.png "0905年 04_IconLocation")

 **可接受的变体字段验证图标位置**

#### <a name="validation-requiring-a-round-trip-to-a-server-or-network-connection"></a>验证需要往返于服务器或网络连接
 在某些情况下，到服务器的往返行程时需要验证其内容，并有一点很重要，显示用户进度，验证和错误状态。 下图显示了此用例和推荐的 UI 的示例。

 ![验证涉及到一台服务器的往返行程](../../extensibility/ux-guidelines/media/0905-05_roundtrip.png "0905年 05_RoundTrip")

 **验证涉及到一台服务器的往返行程**

 请注意，必须以适应的"验证..."和"重试"文本提供足够的可用空间，右侧的控件。

#### <a name="in-place-warning-text"></a>就地警告文本
 当有空间可用于将接近控件的错误消息放在错误的状态时，最好是使用单独的工具提示。

 ![在&#45;放置警告](../../extensibility/ux-guidelines/media/0905-06_inplacewarning.png "0905年 06_InPlaceWarning")

 **就地警告文本**

#### <a name="watermarks"></a>水印
 有时整个控件或窗口处于错误状态。 在此情况下，使用水印来指示错误。

 ![Watermark](../../extensibility/ux-guidelines/media/0905-07_watermark.png "0905-07_Watermark")

 **水印字段验证**