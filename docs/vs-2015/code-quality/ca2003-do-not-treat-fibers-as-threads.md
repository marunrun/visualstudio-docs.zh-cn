---
title: CA2003：不要将纤程视为线程 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2003
- DoNotTreatFibersAsThreads
helpviewer_keywords:
- CA2003
- DoNotTreatFibersAsThreads
ms.assetid: 15398fb1-f384-4bcc-ad93-00e1c0fa9ddf
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a8172490b267949686dd3390c85ed6d86531b192
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85521169"
---
# <a name="ca2003-do-not-treat-fibers-as-threads"></a>CA2003:不要将纤程视为线程
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|DoNotTreatFibersAsThreads|
|CheckId|CA2003|
|类别|Microsoft 可靠性|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 托管线程被视为 Win32 线程。

## <a name="rule-description"></a>规则描述
 不要假设托管线程是 Win32 线程。 它是一个纤程。 公共语言运行时（CLR）将在 SQL 拥有的实际线程的上下文中将托管线程作为纤程运行。 这些线程可以在 Appdomain 甚至是 SQL Server 进程中的数据库之间共享。 使用托管线程本地存储可正常运行，但不能使用非托管线程本地存储，也不会假设你的代码将再次在当前 OS 线程上运行。 不要更改设置，例如线程的区域设置。 不要通过 P/Invoke 调用 CreateCriticalSection 或 CreateMutex，因为它们要求进入锁定的线程还必须退出锁。 由于使用纤程时不会出现这种情况，因此在 SQL 中将不会用到 Win32 关键部分和互斥体。 您可以安全地在托管的系统上使用大部分状态。 这包括托管线程本地存储和线程的当前用户界面（UI）区域性。 然而，出于编程模型的原因，使用 SQL 时将无法更改线程的当前区域性;这将通过新的权限强制执行。

## <a name="how-to-fix-violations"></a>如何解决冲突
 检查线程的使用情况，并相应地更改代码。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不应禁止显示此规则。
