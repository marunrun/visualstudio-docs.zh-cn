---
title: CA2228:不要发行未发布的资源格式
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotShipUnreleasedResourceFormats
- CA2228
helpviewer_keywords:
- CA2228
- DoNotShipUnreleasedResourceFormats
ms.assetid: 2c614edc-4e94-4b4f-8067-eea677a75cd9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5f8a672056c8663c2e27ec730e542083aee9738f
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66714978"
---
# <a name="ca2228-do-not-ship-unreleased-resource-formats"></a>CA2228:不要发行未发布的资源格式

|||
|-|-|
|TypeName|DoNotShipUnreleasedResourceFormats|
|CheckId|CA2228|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

使用当前不支持的.NET 版本的生成资源文件。

## <a name="rule-description"></a>规则说明

通过使用.NET 的预发布版本生成的资源文件可能不是可由支持的.NET 版本。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，生成使用受支持的.NET 版本的资源。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。
