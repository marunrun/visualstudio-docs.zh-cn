---
title: '&lt;&gt; (引导程序) 计划元素 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <Schedules> element [bootstrapper]
ms.assetid: 28d094cf-64f5-42b1-bd8a-3697082aab4f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a2f6e4ae90dbd36dab4f4df7f72d5ecf57ee04b1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62927327"
---
# <a name="ltschedulesgt-element-bootstrapper"></a>&lt;计划 &gt; 元素 (引导程序) 
`Schedules`元素包含 `Schedule` 元素，这些元素定义应在哪些特定时间运行元素定义的命令 `Command` 。

## <a name="syntax"></a>语法

```xml
<Schedules>
    <Schedule
        Name
    >
        <BuildList />
        <BeforePackage />
        <AfterPackage />
    </Schedule>
</Schedules>
```

## <a name="elements-and-attributes"></a>元素和属性
 `Schedules`元素是元素的子元素 `Product` 。 每个 `Product` 元素最多只能有一个 `Schedules` 元素。 `Schedules` 元素没有属性。

## <a name="schedule"></a>计划
 `Schedule`元素是元素的子元素 `Schedules` 。 `Schedules`元素必须至少有一个 `Schedule` 元素。

 `Schedule` 具有以下属性。

|特性|说明|
|---------------|-----------------|
|`Name`|必需。 计划项的名称。 这与元素的 `ScheduleName` 属性相对应 `Command` 。 当 `Command` 引用命名计划时，它将仅在该元素指示的时间执行 `Schedule` 。 计划还可能与 `FailIf` 和 `BypassIf` 元素关联，这些元素限制这些条件测试按指定的计划执行。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|

 某个给定 `Schedule` 元素可能正好具有以下子级之一。

## <a name="buildlist"></a>BuildList
 `BuildList`元素指示安装程序在启动引导应用程序之后立即执行命令。

## <a name="beforepackage"></a>BeforePackage
 `BeforePackage`元素指示安装程序在安装指定的包之前执行命令。

## <a name="afterpackage"></a>AfterPackage
 `AfterPackage`元素指示安装程序在安装指定的包后执行命令。

## <a name="see-also"></a>另请参阅
- [\<Product> element](../deployment/product-element-bootstrapper.md)
- [产品和包架构引用](../deployment/product-and-package-schema-reference.md)