---
title: T4 CleanUpBehavior 指令
description: 了解 CleanUpBehavior 指令以及如何在处理文本模板后删除 appDomain。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9c07d0bf714d42cc605d76d593ed48a70b925483
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2020
ms.locfileid: "97363674"
---
# <a name="t4-cleanupbehavior-directive"></a>T4 CleanUpBehavior 指令

若要在处理文本模板之后删除 appDomain，请包括以下行：

```
<#@ CleanupBehavior processor="T4VSHost" CleanupAfterProcessingtemplate="true" #>
```

文本模板是在独立于主机进程之外的 appDomain 中进行处理的。 在大多数情况下，在处理了一个文本模板之后，则将再次使用 appdomain 处理下一个模板。 但如果你指定 CleanupBehavior，则将删除 appDomain 并且将在新的 appDomain 中处理下一个模板。

这将减慢文本处理的速度，但可用于确保释放资源。

此指令将仅在 Visual Studio 主机中起作用。
