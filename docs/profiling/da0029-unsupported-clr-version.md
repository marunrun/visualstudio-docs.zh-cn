---
title: DA0029：不支持的 CLR 版本 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.29
- vs.performance.rules.DA0029
helpviewer_keywords:
- vs.performance.29
- vs.performance.DA0029
- vs.performance.rules.DA0029
ms.assetid: 76247259-c6f3-44c4-b3f9-d8dac16b5e0d
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: dbc0bfcdb49557e56711b60dca11977a3504d907
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74777510"
---
# <a name="da0029-unsupported-clr-version"></a>DA0029：不支持的 CLR 版本

|||
|-|-|
|规则 ID|DA0029|
|类别|分析工具使用情况|
|分析方法|从命令行分析|
|消息|在收集期间检测到不受支持的 CLR 版本。 托管符号可能无法正确解析。|
|规则类型|信息。|

## <a name="cause"></a>原因
 尝试分析的应用程序使用的 [!INCLUDE[net_v11_long](../profiling/includes/net_v11_long_md.md)] 不受分析工具支持。

## <a name="rule-description"></a>规则说明
 出现此警告是因为，分析工具不能解析在应用程序中运行的托管代码符号。 分析工具无法解析运行 [!INCLUDE[net_v11_long](../profiling/includes/net_v11_long_md.md)] 的应用程序的托管代码符号。

## <a name="how-to-fix-violations"></a>如何解决冲突
 无。
