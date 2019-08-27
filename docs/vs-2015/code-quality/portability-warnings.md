---
title: 可移植性警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.PortabilityRules
helpviewer_keywords:
- portability warnings
- managed code analysis warnings, portability warnings
- warnings, portability
ms.assetid: 902e859a-2153-4970-baaa-8a5b4a11806f
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 7c8f195f2219cfa2c81b24a3e04ddc559dc98a06
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142213"
---
# <a name="portability-warnings"></a>可移植性警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可移植性警告支持跨不同操作系统的可移植性。  
  
## <a name="in-this-section"></a>本节内容  
  
|规则|描述|  
|----------|-----------------|  
|[CA1900:值类型字段应为可移植](../code-quality/ca1900-value-type-fields-should-be-portable.md)|此规则检查： 当用显式布局特性声明的结构封送到 64 位操作系统上的非托管代码时，将正确对齐。|  
|[CA1901:P/Invoke 声明应为可移植](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)|此规则计算每个参数的大小和 P/Invoke 的返回值，并验证它们的大小正确封送到 32 位和 64 位操作系统上的非托管代码时。|  
|[CA1903:使用仅目标框架中的 API](../code-quality/ca1903-use-only-api-from-targeted-framework.md)|一个成员或类型使用了某个 Service Pack 中引入的成员或类型，该 Service Pack 没有与项目的目标框架一起包括。|
