---
title: CA2228：不提供未发布资源格式 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotShipUnreleasedResourceFormats
- CA2228
helpviewer_keywords:
- CA2228
- DoNotShipUnreleasedResourceFormats
ms.assetid: 2c614edc-4e94-4b4f-8067-eea677a75cd9
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4adcae1c1cc616cdbcf5a7aa15342d221c2f4300
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540577"
---
# <a name="ca2228-do-not-ship-unreleased-resource-formats"></a>CA2228:不要发行未发布的资源格式
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|DoNotShipUnreleasedResourceFormats|
|CheckId|CA2228|
|Category|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 资源文件是使用 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 当前不受支持的版本生成的。

## <a name="rule-description"></a>规则描述
 使用的预发行版本生成的资源文件 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 可能无法由 .NET Framework 的受支持版本使用。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用支持的 k 版本创建资源 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。
