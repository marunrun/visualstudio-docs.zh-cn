---
title: 任务类 - 内部成员 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712739"
---
# <a name="task-class---internal-members"></a>任务类 - 内部成员
本文介绍了帮助您实现自定义调试器的<xref:System.Threading.Tasks.Task?displayProperty=fullName>类的内部成员。 有关此类的一般信息，<xref:System.Threading.Tasks.Task>请参阅参考文章。

 **命名空间：**<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集**：mscorlib（在*mscorlib.dll*中）

 由于您无法从 .NET 框架访问这些内部成员，因此在通用中间语言 （CIL） 中提供了以下语法。

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
|[SetNotificationForWaitCompletion 方法](../../extensibility/debugger/setnotificationforwaitcompletion-method.md)|设置或清除TASK_STATE_WAIT_COMPLETION_NOTIFICATION状态位。|
|[NotifyDebuggerOfWaitCompletion 方法](../../extensibility/debugger/notifydebuggerofwaitcompletion-method.md)|占位符方法用作调试器的断点目标。|

### <a name="fields"></a>字段

|名称|描述|
|----------|-----------------|
|[m_action](../../extensibility/debugger/m-action-field.md)|表示要在对象中执行的代码的<xref:System.Threading.Tasks.Task>委托。|
|[m_contingentProperties](../../extensibility/debugger/m-contingentproperties-field.md)|存储<xref:System.Threading.Tasks.Task>对象的其他属性。|
|[m_parent](../../extensibility/debugger/m-parent-field.md)|父属性的<xref:System.Threading.Tasks.Task?displayProperty=fullName>备份字段。|
|[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)|存储有关<xref:System.Threading.Tasks.Task>对象当前状态的信息。|
|[m_stateObject](../../extensibility/debugger/m-stateobject-field.md)|表示操作将使用的数据的对象。|
|[m_taskId](../../extensibility/debugger/m-taskid-field.md)|属性的<xref:System.Threading.Tasks.Task.Id%2A?displayProperty=fullName>后备字段。|
|[s_taskIdCounter](../../extensibility/debugger/s-taskidcounter-field.md)|对象的下一个<xref:System.Threading.Tasks.Task>可用标识符。|
|[TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)|指示任务在到达运行状态之前已取消，或者任务确认其取消并无异常地完成。|
|[TASK_STATE_EXECUTED](../../extensibility/debugger/task-state-executed-field.md)|指示任务正在运行。|
|[TASK_STATE_FAULTED](../../extensibility/debugger/task-state-faulted-field.md)|指示任务由于未处理的异常而已完成。|
|[TASK_STATE_RAN_TO_COMPLETION](../../extensibility/debugger/task-state-ran-to-completion-field.md)|指示任务成功完成执行。|
|[TASK_STATE_WAITING_ON_CHILDREN](../../extensibility/debugger/task-state-waiting-on-children-field.md)|指示任务已完成执行其委托，并隐式等待附加的子任务完成。|

## <a name="remarks"></a>备注
 以下内部方法对调试器引擎很有用，因为它们标记了代码执行的入口<xref:System.Threading.Tasks.Task>：

- `Execute`

- `ExecuteEntry`

- `ExecuteWithThreadLocal`

- `Finish`

- `InnerInvoke`

- `InternalWait`

## <a name="see-also"></a>请参阅
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- [.NET 框架的并行扩展内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
