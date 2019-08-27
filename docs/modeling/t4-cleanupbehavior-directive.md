---
title: T4 CleanUpBehavior 指令
ms.date: 11/04/2016
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 27df15c0b935ff4bae497940c095dba1598bc4c1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62964100"
---
# <a name="t4-cleanupbehavior-directive"></a>T4 CleanUpBehavior 指令

若要在处理文本模板之后删除 appDomain，请包括以下行：

```
<#@ CleanupBehavior processor="T4VSHost" CleanupAfterProcessingtemplate="true" #>
```

文本模板是在独立于主机进程之外的 appDomain 中进行处理的。 在大多数情况下，在处理了一个文本模板之后，则将再次使用 appdomain 处理下一个模板。 但如果你指定 CleanupBehavior，则将删除 appDomain 并且将在新的 appDomain 中处理下一个模板。

这将减慢文本处理的速度，但可用于确保释放资源。

此指令将仅在 Visual Studio 主机中起作用。