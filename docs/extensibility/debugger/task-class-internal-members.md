---
title: Task 类-内部成员 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, Task class [.NET Framework]
- Task class [.NET Framework debug engines]
ms.assetid: 28e47c3b-9323-424a-80ac-6cc3bf19e09b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3bfa171655afd808de4bd86fe0fbdb99531d2ab2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348427"
---
# <a name="task-class---internal-members"></a>任务类-内部成员
本文介绍的内部成员的<xref:System.Threading.Tasks.Task?displayProperty=fullName>类，可帮助您实现自定义调试器。 有关此类的常规信息，请参阅<xref:System.Threading.Tasks.Task>参考文章。

 **Namespace**：<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：** mscorlib (在*mscorlib.dll*)

 无法从.NET Framework 来访问这些内部成员，因为以下语法提供通用中间语言 (CIL)。

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

|名称|描述|
|----------|-----------------|
|[SetNotificationForWaitCompletion 方法](../../extensibility/debugger/setnotificationforwaitcompletion-method.md)|设置或清除 TASK_STATE_WAIT_COMPLETION_NOTIFICATION 状态位。|
|[NotifyDebuggerOfWaitCompletion 方法](../../extensibility/debugger/notifydebuggerofwaitcompletion-method.md)|由调试器使用断点目标的占位符方法。|

### <a name="fields"></a>字段

|名称|描述|
|----------|-----------------|
|[m_action](../../extensibility/debugger/m-action-field.md)|表示要在中执行的代码的委托<xref:System.Threading.Tasks.Task>对象。|
|[m_contingentProperties](../../extensibility/debugger/m-contingentproperties-field.md)|将存储的其他属性<xref:System.Threading.Tasks.Task>对象。|
|[m_parent](../../extensibility/debugger/m-parent-field.md)|有关支持字段<xref:System.Threading.Tasks.Task?displayProperty=fullName>父属性。|
|[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)|存储的当前状态有关的信息<xref:System.Threading.Tasks.Task>对象。|
|[m_stateObject](../../extensibility/debugger/m-stateobject-field.md)|一个对象，表示将由该操作使用的数据。|
|[m_taskId](../../extensibility/debugger/m-taskid-field.md)|有关支持字段<xref:System.Threading.Tasks.Task.Id%2A?displayProperty=fullName>属性。|
|[s_taskIdCounter](../../extensibility/debugger/s-taskidcounter-field.md)|下一步提供标识符<xref:System.Threading.Tasks.Task>对象。|
|[TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)|指示该任务被取消之前它已达到运行状态，或任务确认其取消和完成且未出现异常。|
|[TASK_STATE_EXECUTED](../../extensibility/debugger/task-state-executed-field.md)|指示任务正在运行。|
|[TASK_STATE_FAULTED](../../extensibility/debugger/task-state-faulted-field.md)|指示任务已完成，由于未经处理的异常。|
|[TASK_STATE_RAN_TO_COMPLETION](../../extensibility/debugger/task-state-ran-to-completion-field.md)|指示任务已成功完成执行。|
|[TASK_STATE_WAITING_ON_CHILDREN](../../extensibility/debugger/task-state-waiting-on-children-field.md)|指示任务完成执行其委托和隐式等待附加的子任务完成。|

## <a name="remarks"></a>备注
 以下内部方法非常有用到调试器引擎，因为它们标记为 entrance<xref:System.Threading.Tasks.Task>代码执行：

- `Execute`

- `ExecuteEntry`

- `ExecuteWithThreadLocal`

- `Finish`

- `InnerInvoke`

- `InternalWait`

## <a name="see-also"></a>请参阅
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- [.NET Framework 的并行扩展内幕](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)