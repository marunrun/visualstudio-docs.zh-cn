---
title: 调试 UWP 时触发挂起/继续/后台事件
ms.custom: seodec18
ms.date: 01/16/2018
ms.topic: how-to
f1_keywords:
- vs.debug.error.background_task_activate_failure
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 83b4bea32f642cbf48acb01831bd4bccc2bb15a0
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348933"
---
# <a name="how-to-trigger-suspend-resume-and-background-events-while-debugging-uwp-apps-in-visual-studio"></a>在 Visual Studio 中调试 UWP 应用时如何触发挂起、继续和后台事件

不调试时，Windows **进程生命期管理** (PLM) 根据用户操作和设备状态控制应用程序的执行状态 - 启动、挂起、继续和终止应用程序。 在调试时，Windows 禁用这些激活事件。 本主题介绍如何在调试器中触发这些事件。

本主题还介绍如何调试 **后台任务**。 借助后台任务，即使应用未在运行，也可在后台进程中执行某些操作。 可使用调试器使应用程序进入调试模式，然后不启动 UI 即启动和调试后台任务。

有关进程生存期管理和后台任务的详细信息，请参阅[启动、继续和多任务处理](/windows/uwp/launch-resume/index)。

## <a name="trigger-process-lifetime-management-events"></a><a name="BKMK_Trigger_Process_Lifecycle_Management_events"></a> 触发进程生命期管理事件
 当用户从应用切换至别处时或当 Windows 进入电量不足状态时，Windows 可挂起应用。 可响应 `Suspending` 事件，将相关的应用程序和用户数据保存到永久存储并释放资源。 从 **“已挂起”** 状态继续应用程序时，该应用程序将进入 **“正在运行”** 状态，并从其挂起之处继续。 可响应 `Resuming` 事件，还原或刷新应用程序状态并回收资源。

 尽管 Windows 尝试尽可能多地在内存中保留挂起的应用程序，但如果没有足够资源可将应用程序保留在内存中，则 Windows 仍可终止该应用程序。 用户还可显式关闭应用程序。 没有特殊事件指示用户已关闭应用程序。

 在 Visual Studio 调试器中，可手动挂起、继续和终止应用程序以调试进程生命周期事件。 若要调试进程生命周期事件，请执行以下操作：

1. 在要调试的事件的处理程序中设置断点。

2. 按 **F5** 启动调试。

3. 在 **“调试位置”** 工具栏上，选择要触发的事件：

     ![挂起、继续、终止和后台执行任务](../debugger/media/dbg_suspendresumebackground.png)

     “挂起和终止”将关闭应用并结束调试会话。

## <a name="trigger-background-tasks"></a><a name="BKMK_Trigger_background_tasks"></a> 触发后台任务
 任何应用程序均可注册后台任务以响应某些系统事件，即使应用程序未运行也是如此。 后台任务不能运行直接更新 UI 的代码，但可通过磁贴更新、徽章更新和 toast 通知向用户显示信息。 有关详细信息，请参阅[使用后台任务支持应用](https://msdn.microsoft.com/library/4c7bb148-eb1f-4640-865e-41f627a46e8e)。

 可从调试器触发对应用程序启动后台任务的事件。

> [!NOTE]
> 调试器只能触发那些不包含数据的事件，如指示设备中状态更改的事件。 必须手动触发需要用户输入或其他数据的后台任务。

 触发后台任务事件的最实际的方法是在应用程序未运行时触发。 但是，也支持在标准调试会话中触发该事件。

### <a name="trigger-a-background-task-event-from-a-standard-debug-session"></a><a name="BKMK_Trigger_a_background_task_event_from_a_standard_debug_session"></a> 从标准调试会话中触发后台任务事件

1. 在要调试的后台任务代码中设置断点。

2. 按 **F5** 启动调试。

3. 从 **“调试位置”** 工具栏上的事件列表中，选择要启动的后台任务。

     ![挂起、继续、终止和后台执行任务](../debugger/media/dbg_suspendresumebackground.png)

### <a name="trigger-a-background-task-when-the-app-is-not-running"></a><a name="BKMK_Trigger_a_background_task_when_the_app_is_not_running"></a> 在应用程序未运行时触发后台任务

1. 在要调试的后台任务代码中设置断点。

2. 打开启动项目的调试属性页。 在“解决方案资源管理器”中，选择项目。 在 **“调试”** 菜单中，选择 **“属性”** 。

     对于 C++ 项目，展开“配置属性”，然后选择“调试”。

3. 执行下列操作之一：

    - 对于 Visual C# 和 Visual Basic 项目，选择 **“不启动，但在启动时调试代码”**

         ![C#/VB 调试启动应用程序属性](../debugger/media/dbg_csvb_dontlaunchapp.png "DBG_CsVb_DontLaunchApp")

    - 对于 C++ 项目，从“启动应用程序”列表中选择“否”。

         ![C++/VB 启动应用程序调试属性](../debugger/media/dbg_cppjs_dontlaunchapp.png "DBG_CppJs_DontLaunchApp")

4. 按 **F5** 使应用程序进入调试模式。 注意， **“调试位置”** 工具栏上的 **“进程”** 列表显示应用程序包名称以指示您处于调试模式下。

     ![后台任务进程列表](../debugger/media/dbg_backgroundtask_processlist.png "DBG_BackgroundTask_ProcessList")

5. 从 **“调试位置”** 工具栏上的事件列表中，选择要启动的后台任务。

     ![挂起、继续、终止和后台任务](../debugger/media/dbg_suspendresumebackground.png "DBG_SuspendResumeBackground")

## <a name="trigger-process-lifetime-management-events-and-background-tasks-from-an-installed-app"></a><a name="BKMK_Trigger_Process_Lifetime_Management_events_and_background_tasks_from_an_installed_app"></a> 从安装的应用程序中触发进程生命期管理事件和后台任务
 使用“调试安装的应用包”对话框加载已安装到调试器中的应用。 例如，你可以调试已从 Microsoft Store 安装的应用，或在具有应用的源文件但没有针对应用的 Visual Studio 项目时调试应用。 利用“调试安装的应用包”对话框，你可以在 Visual Studio 计算机或远程设备上在调试模式下启动应用，也可以将应用设置为在调试模式下运行但不启动应用。 有关详细信息，请参阅[调试安装的应用包](../debugger/debug-installed-app-package.md)。

 在将应用程序加载到调试器中后，您可以使用上述任意过程。

## <a name="diagnosing-background-task-activation-errors"></a><a name="BKMK_Diagnosing_background_task_activation_errors"></a> 诊断后台任务激活错误
 Windows 事件查看器中针对后台基础结构的诊断日志包含详细信息，这些信息可用于诊断和排查后台任务错误。 若要查看日志，请执行以下操作：

1. 打开事件查看器应用程序。

2. 在 **“操作”** 窗格中，选择 **“查看”** ，然后确保选中 **“显示分析和调试日志”** 。

3. 在 **“事件查看器(本地)”** 树中，依次展开 **“应用程序和服务日志”**  >  **“Microsoft”**  >  **“Windows”**  >  **“BackgroundTasksInfrastructure”** 。

4. 选择 **“诊断”** 日志。

## <a name="see-also"></a>请参阅
- [使用 Visual Studio 测试 UWP 应用](/visualstudio/test/create-and-run-unit-tests-for-a-store-app-in-visual-studio)
- [在 Visual Studio 中调试应用](debugging-windows-store-and-windows-universal-apps.md)
- [应用程序生命周期](/windows/uwp/launch-resume/app-lifecycle)
- [Launching, resuming, and multitasking](/windows/uwp/launch-resume/index)