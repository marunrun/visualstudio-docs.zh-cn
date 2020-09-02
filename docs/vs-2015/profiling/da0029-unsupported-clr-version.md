---
title: DA0029：不支持的 CLR 版本 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.29
- vs.performance.rules.DA0029
helpviewer_keywords:
- vs.performance.29
- vs.performance.DA0029
- vs.performance.rules.DA0029
ms.assetid: 76247259-c6f3-44c4-b3f9-d8dac16b5e0d
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 532427618f476e1e187d8a1c88749810f9d157c9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152646"
---
# <a name="da0029-unsupported-clr-version"></a>DA0029：CLR 版本不受支持
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

规则 Id |DA0029 |  
|类别 |分析工具使用情况 |  
|分析方法 |从命令行分析 |  
|消息 |在收集过程中检测到不受支持的 CLR 版本。 托管符号可能无法正确解析。|  
|规则类型 |信息。 |  
  
## <a name="cause"></a>原因  
 尝试分析的应用程序使用的 [!INCLUDE[net_v11_long](../includes/net-v11-long-md.md)] 不受分析工具支持。  
  
## <a name="rule-description"></a>规则描述  
 出现此警告是因为，分析工具不能解析在应用程序中运行的托管代码符号。 分析工具无法解析运行 [!INCLUDE[net_v11_long](../includes/net-v11-long-md.md)] 的应用程序的托管代码符号。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 无。
