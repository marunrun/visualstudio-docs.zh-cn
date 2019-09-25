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
ms.openlocfilehash: 9f5e4e7eb28207cb37824b23acbbac02b6df380d
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233133"
---
# <a name="ca2003-do-not-treat-fibers-as-threads"></a>CA2003:不要将纤程视为线程

|||
|-|-|
|TypeName|DoNotTreatFibersAsThreads|
|CheckId|CA2003|
|类别|Microsoft.Reliability|
|重大更改|不间断|

## <a name="cause"></a>原因

托管线程被视为 Win32 线程。

## <a name="rule-description"></a>规则说明

不要假设托管线程是 Win32 线程;这是一种纤程。 公共语言运行时（CLR）将托管线程作为纤程运行在由 SQL 拥有的实际线程的上下文中。 这些线程可以在 Appdomain 甚至是 SQL Server 进程中的数据库之间共享。 使用托管线程本地存储可以正常工作，但不能使用非托管线程本地存储，也不会假设你的代码将再次在当前 OS 线程上运行。 不要更改设置，例如线程的区域设置。 不要通过 P/Invoke 调用 CreateCriticalSection 或 CreateMutex，因为它们要求进入锁定的线程还必须退出锁。 因为当你使用纤程时，进入锁定的线程不会退出锁定，而 Win32 临界区和互斥体在 SQL 中毫无用处。 您可以安全地在托管<xref:System.Threading.Thread>对象上使用大部分状态，包括托管线程本地存储和线程的当前用户界面（UI）区域性。 然而，出于编程模型的原因，使用 SQL 时将无法更改线程的当前区域性。 此限制将通过新权限强制执行。

## <a name="how-to-fix-violations"></a>如何解决冲突

检查线程的使用情况，并相应地更改代码。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

请勿禁止显示此规则。