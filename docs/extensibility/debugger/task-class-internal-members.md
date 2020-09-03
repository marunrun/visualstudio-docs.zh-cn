---
title: 任务类-内部成员 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, Task class [.NET Framework]
- Task class [.NET Framework debug engines]
ms.assetid: 28e47c3b-9323-424a-80ac-6cc3bf19e09b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dcf278c0248b344cea4be7cf161ecc91581f5f2e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80712739"
---
# <a name="task-class---internal-members"></a>任务类-内部成员
本文介绍 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 可帮助你实现自定义调试器的类的内部成员。 有关此类的常规信息，请参阅 <xref:System.Threading.Tasks.Task> 参考文章。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly：** mscorlib (*mscorlib.dll*) 

 由于不能从 .NET Framework 访问这些内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.class public auto ansi System.Threading.Tasks.Task
       extends System.Object
       implements System.Threading.IThreadPoolWorkItem,
                  System.IAsyncResult,
                  System.IDisposable,
                  System.Threading.ICancelableOperation
```

## <a name="members"></a>成员

### <a name="methods"></a>方法

|名称|说明|
|----------|-----------------|
|[SetNotificationForWaitCompletion 方法](../../extensibility/debugger/setnotificationforwaitcompletion-method.md)|设置或清除 TASK_STATE_WAIT_COMPLETION_NOTIFICATION 状态位。|
|[NotifyDebuggerOfWaitCompletion 方法](../../extensibility/debugger/notifydebuggerofwaitcompletion-method.md)|调试器使用的占位符方法作为断点目标。|

### <a name="fields"></a>字段

|名称|说明|
|----------|-----------------|
|[m_action](../../extensibility/debugger/m-action-field.md)|委托，它表示要在对象中执行的代码 <xref:System.Threading.Tasks.Task> 。|
|[m_contingentProperties](../../extensibility/debugger/m-contingentproperties-field.md)|存储对象的附加属性 <xref:System.Threading.Tasks.Task> 。|
|[m_parent](../../extensibility/debugger/m-parent-field.md)|父属性的支持字段 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 。|
|[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)|存储有关对象的当前状态的信息 <xref:System.Threading.Tasks.Task> 。|
|[m_stateObject](../../extensibility/debugger/m-stateobject-field.md)|一个对象，它表示将由操作使用的数据。|
|[m_taskId](../../extensibility/debugger/m-taskid-field.md)|属性的支持字段 <xref:System.Threading.Tasks.Task.Id%2A?displayProperty=fullName> 。|
|[s_taskIdCounter](../../extensibility/debugger/s-taskidcounter-field.md)|对象的下一个可用标识符 <xref:System.Threading.Tasks.Task> 。|
|[TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)|指示任务在达到运行状态之前已取消，或任务已确认其取消并完成而不发生异常。|
|[TASK_STATE_EXECUTED](../../extensibility/debugger/task-state-executed-field.md)|指示任务正在运行。|
|[TASK_STATE_FAULTED](../../extensibility/debugger/task-state-faulted-field.md)|指示由于未处理的异常而完成的任务。|
|[TASK_STATE_RAN_TO_COMPLETION](../../extensibility/debugger/task-state-ran-to-completion-field.md)|指示任务已成功完成执行。|
|[TASK_STATE_WAITING_ON_CHILDREN](../../extensibility/debugger/task-state-waiting-on-children-field.md)|指示任务已完成执行其委托并隐式等待附加的子任务完成。|

## <a name="remarks"></a>备注
 以下内部方法对于调试器引擎非常有用，因为它们将入口标记为 <xref:System.Threading.Tasks.Task> 代码执行：

- `Execute`

- `ExecuteEntry`

- `ExecuteWithThreadLocal`

- `Finish`

- `InnerInvoke`

- `InternalWait`

## <a name="see-also"></a>另请参阅
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- [.NET Framework 的并行扩展内部机制](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
