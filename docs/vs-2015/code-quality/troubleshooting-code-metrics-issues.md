---
title: 代码度量问题疑难解答 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: troubleshooting
ms.assetid: f2fdb995-4888-4246-85dc-7bacadd45968
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 1567715a8f944eb10c2728caa9fc1edd43beda8e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62580578"
---
# <a name="troubleshooting-code-metrics-issues"></a>代码度量值问题疑难解答
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

收集代码度量时，可能会遇到以下的一些问题：  
  
- [Visual Studio 2010 代码复杂度计算中的更改](#Changes_in_Visual_Studio_2010_code_complexity_calculations)  
  
## <a name="Changes_in_Visual_Studio_2010_code_complexity_calculations"></a>Visual Studio 2010 代码复杂度计算中的更改  
 对于相同的函数，在以下情况下，[!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] 中计算的代码复杂度度量可以不同于早期版本的 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 计算的度量：  
  
- 此函数包含一个或多个 catch 块。 在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 以前的版本中，catch 块不包含在计算中。 在 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] 中，每个 catch 块的复杂度均添加到函数的复杂度中。  
  
- 此函数包含 switch（VB 中的 Select Case）语句。 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] 和早期版本之间的编译器差异可以为包含失败事例的某些 switch 语句生成不同的 MSIL 代码。  
  
## <a name="see-also"></a>请参阅  
 [测量托管代码的复杂性和可维护性](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)
