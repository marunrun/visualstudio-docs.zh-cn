---
title: Annotating Locking Behavior | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _Releases_nonreentrant_lock_
- _Lock_kind_mutex_
- _Lock_kind_critical_section_
- _Acquires_lock_
- _Releases_lock_
- _Has_lock_kind_
- _Releases_exclusive_lock_
- _Post_same_lock_
- _Requires_exclusive_lock_held_
- _Requires_shared_lock_held_
- _Lock_kind_semaphore_
- _Requires_lock_held_
- _Acquires_exclusive_lock_
- _Create_lock_level_
- _Acquires_nonreentrant_lock_
- _Releases_shared_lock_
- _Has_lock_level_
- _Lock_kind_spin_lock_
- _Requires_lock_not_held_
- _Acquires_shared_lock_
- _Requires_no_locks_held_
- _Lock_level_order_
- _Lock_kind_event_
ms.assetid: 07769c25-9b97-4ab7-b175-d1c450308d7a
caps.latest.revision: 11
author: mikeblome
ms.author: mblome
manager: jillfra
ms.openlocfilehash: a5b34253485da233ba6e25841b6592068de6fb69
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295831"
---
# <a name="annotating-locking-behavior"></a>对锁定行为进行批注
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要避免多线程程序中的并发 Bug，请遵循适当的锁定规则并使用 SAL 批注。  
  
 并发 Bug 很难重现、诊断和调试，因为它们是非确定性的。 有关线程交错的推理是最困难的，如果设计包含多个线程的代码体，这会变得不切实际。 因此，最好在多线程程序中遵循锁定规则。 例如，在获取多个锁时遵守锁定顺序可以帮助避免死锁，在访问共享资源之前获取适当的保护锁有助于避免争用条件。  
  
 遗憾的是，看似简单的锁定规则在实践中会很难遵循。 当今编程语言和编译器存在一个基本限制，即它们不能直接支持并发需求的规范和分析。 程序员必须依赖于非正式的代码批注来表示他们对于使用锁定的意图。  
  
 并发 SAL 批注用于帮助您指定锁定的副作用、锁定责任、数据保护、锁的顺序层次结构，以及其他预期的锁定行为。 通过将隐式规则设置为显式，SAL 并发批注可提供一致方式，用于说明代码使用锁定规则的方式。 并发批注还可增强代码分析工具查找争用条件、死锁、不匹配的同步操作和其他细微并发错误的能力。  
  
## <a name="general-guidelines"></a>通用准则  
 通过使用批注，您可以显式声明在实现（被调用方）和客户端（调用方）之间通过函数定义隐式使用的协定，并表明程序中可进一步改进分析的固定条件及其他属性。  
  
 SAL 支持许多不同类型的锁定基元，例如临界区、互斥锁、自旋锁和其他资源对象。 许多并发批注采用锁表达式作为参数。 按照约定，锁由基础锁对象的路径表达式表示。  
  
 应记住的一些线程所有权规则：  
  
- 自旋锁是具有明确线程所有权的非计数锁。  
  
- 互斥锁和临界区是具有明确线程所有权的计数锁。  
  
- 信号量和事件是不具有明确线程所有权的计数锁。  
  
## <a name="locking-annotations"></a>锁定批注  
 下表列出了锁定批注。  
  
|批注|描述|  
|----------------|-----------------|  
|`_Acquires_exclusive_lock_(expr)`|批注函数并表明在状态后，函数会将 `expr` 命名的锁对象的排他锁计数递增 1。|  
|`_Acquires_lock_(expr)`|批注函数并表明在状态后，函数会将 `expr` 命名的锁对象的锁计数递增 1。|  
|`_Acquires_nonreentrant_lock_(expr)`|已获得由 `expr` 命名的锁。  如果已拥有此锁，会报告错误。|  
|`_Acquires_shared_lock_(expr)`|批注函数并表明在状态后，函数会将 `expr` 命名的锁对象的共享锁计数递增 1。|  
|`_Create_lock_level_(name)`|该语句声明符号 `name` 为锁级别，因此可以在批注 `_Has_Lock_level_` 和 `_Lock_level_order_` 中使用。|  
|`_Has_lock_kind_(kind)`|批注所有对象以优化资源对象的类型信息。 有时一种通用类型会用于不同类型的资源，并且重载的类型不足以区分各资源之间的语义需求。 下面提供了一个预定义 `kind` 参数的列表：<br /><br /> `_Lock_kind_mutex_`<br /> 互斥锁的锁类型 ID。<br /><br /> `_Lock_kind_event_`<br /> 事件的锁类型 ID。<br /><br /> `_Lock_kind_semaphore_`<br /> 信号量的锁类型 ID。<br /><br /> `_Lock_kind_spin_lock_`<br /> 自旋锁的锁类型 ID。<br /><br /> `_Lock_kind_critical_section_`<br /> 临界区的锁类型 ID。|  
|`_Has_lock_level_(name)`|批注锁对象并赋予其 `name` 锁级别。|  
|`_Lock_level_order_(name1, name2)`|该语句提供 `name1` 和 `name2` 之间的锁排序。|  
|`_Post_same_lock_(expr1, expr2)`|批注函数并表明在状态后，两个锁 `expr1` 和 `expr2` 被视为相同的锁对象。|  
|`_Releases_exclusive_lock_(expr)`|批注函数并表明在状态后，函数会将 `expr` 命名的锁对象的排他锁计数递减 1。|  
|`_Releases_lock_(expr)`|批注函数并表明在状态后，函数会将 `expr` 命名的锁对象的锁计数递减 1。|  
|`_Releases_nonreentrant_lock_(expr)`|已发布 `expr` 命名的锁。 如果当前不持有此锁，会报告错误。|  
|`_Releases_shared_lock_(expr)`|批注函数并表明在状态后，函数会将 `expr` 命名的锁对象的共享锁计数递减 1。|  
|`_Requires_lock_held_(expr)`|批注函数并表明在状态前，`expr` 命名的对象的锁计数至少为 1。|  
|`_Requires_lock_not_held_(expr)`|批注函数并表明在状态前，`expr` 命名的对象的锁计数为 0。|  
|`_Requires_no_locks_held_`|批注函数并表明检查器已知的所有锁的锁计数为 0。|  
|`_Requires_shared_lock_held_(expr)`|批注函数并表明在状态前，`expr` 命名的对象的共享锁计数至少为 1。|  
|`_Requires_exclusive_lock_held_(expr)`|批注函数并表明在状态前，`expr` 命名的对象的排他锁计数至少为 1。|  
  
## <a name="sal-intrinsics-for-unexposed-locking-objects"></a>非公开锁定对象的 SAL 内部  
 某些锁对象不通过关联锁定函数的实现公开。  下表列出可对在未公开的锁对象上运行的函数启用批注的 SAL 内部变量。  
  
|批注|描述|  
|----------------|-----------------|  
|`_Global_cancel_spin_lock_`|说明取消自旋锁。|  
|`_Global_critical_region_`|说明临界区。|  
|`_Global_interlock_`|说明互锁操作。|  
|`_Global_priority_region_`|说明优先级区域。|  
  
## <a name="shared-data-access-annotations"></a>共享数据访问批注  
 下表列出了用于共享数据访问的批注。  
  
|批注|描述|  
|----------------|-----------------|  
|`_Guarded_by_(expr)`|批注变量并表明变量每次受到访问时，`expr` 命名的锁对象的锁计数至少为 1。|  
|`_Interlocked_`|批注变量，与 `_Guarded_by_(_Global_interlock_)` 等效。|  
|`_Interlocked_operand_`|批注的函数参数是各个互锁函数之一的目标操作数。  这些操作数必须具有特定的附加属性。|  
|`_Write_guarded_by_(expr)`|批注变量并表明变量每次受到修改时，`expr` 命名的锁对象的锁计数至少为 1。|  
  
## <a name="see-also"></a>请参阅  
 [Using SAL Annotations to Reduce C/C++ Code Defects](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [Understanding SAL](../code-quality/understanding-sal.md)   
 [Annotating Function Parameters and Return Values](../code-quality/annotating-function-parameters-and-return-values.md)   
 [Annotating Function Behavior](../code-quality/annotating-function-behavior.md)   
 [Annotating Structs and Classes](../code-quality/annotating-structs-and-classes.md)   
 [Specifying When and Where an Annotation Applies](../code-quality/specifying-when-and-where-an-annotation-applies.md)   
 [Intrinsic Functions](../code-quality/intrinsic-functions.md)   
 [Best Practices and Examples](../code-quality/best-practices-and-examples-sal.md)   
 [Code Analysis Team Blog](https://go.microsoft.com/fwlink/p/?LinkId=251197)
