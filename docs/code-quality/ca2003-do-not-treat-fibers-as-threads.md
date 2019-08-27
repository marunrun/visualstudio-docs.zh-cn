---
title: CA2003:不要将纤程视为线程
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2003
- DoNotTreatFibersAsThreads
helpviewer_keywords:
- CA2003
- DoNotTreatFibersAsThreads
ms.assetid: 15398fb1-f384-4bcc-ad93-00e1c0fa9ddf
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8faaf3c6557065188c795d75ea9bbe4e78998709
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806982"
---
# <a name="ca2003-do-not-treat-fibers-as-threads"></a>CA2003:不要将纤程视为线程

|||
|-|-|
|TypeName|DoNotTreatFibersAsThreads|
|CheckId|CA2003|
|类别|Microsoft.Reliability|
|是否重大更改|非换行|

## <a name="cause"></a>原因

托管的线程是被视为 Win32 线程。

## <a name="rule-description"></a>规则说明

不要假定一个托管的线程是 Win32 线程;它是纤程。 公共语言运行时 (CLR) 作为纤程的实际线程所拥有的 SQL 上下文中运行托管的线程。 在 SQL Server 进程中，可以在应用程序域和甚至数据库之间共享这些线程。 使用托管线程本地存储的工作原理，但不是能使用非托管的线程本地存储区，也不能假定，您的代码将在当前操作系统线程上再次运行。 不要更改如线程的区域设置的设置。 因为它们要求进入锁的线程也必须退出锁，请勿调用 CreateCriticalSection 或通过 P/Invoke CreateMutex。 由于使用纤程时，进入锁的线程不会退出锁，Win32 临界区和互斥是无用的 SQL。 您可以安全地使用大部分状态，对托管<xref:System.Threading.Thread>对象，包括托管的线程本地存储和线程的当前用户界面 (UI) 区域性。 但是，有关编程模型，因此，您将无法使用 SQL 时更改当前线程的区域性。 通过新的权限，将强制实施此限制。

## <a name="how-to-fix-violations"></a>如何解决冲突

检查你的线程的使用情况，并相应地更改您的代码。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不要禁止显示此规则。