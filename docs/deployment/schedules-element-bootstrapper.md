---
title: '&lt;计划&gt;元素 （引导程序） |Microsoft Docs'
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62927327"
---
# <a name="ltschedulesgt-element-bootstrapper"></a>&lt;计划&gt;元素 （引导程序）
`Schedules`元素包含`Schedule`元素，用于定义在定义的命令的特定时间`Command`元素应运行。

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
 `Schedules`元素是子元素的`Product`元素。 每个`Product`元素可能具有最多一个`Schedules`元素。 `Schedules` 元素没有属性。

## <a name="schedule"></a>计划
 `Schedule`元素是子元素的`Schedules`元素。 一个`Schedules`元素必须至少一个`Schedule`元素。

 `Schedule` 具有以下属性。

|特性|描述|
|---------------|-----------------|
|`Name`|必需。 计划项的名称。 这对应于`ScheduleName`属性的`Command`元素。 当`Command`引用指定的计划，在所指示的时间，将仅执行`Schedule`元素。 此外可能与之关联的计划`FailIf`和`BypassIf`元素，将这些条件测试限制为按指定计划执行。 有关详细信息，请参阅[\<命令 > 元素](../deployment/commands-element-bootstrapper.md)。|

 给定`Schedule`元素可能具有一个以下子节点。

## <a name="buildlist"></a>BuildList
 `BuildList`元素指示安装程序以引导应用程序启动后立即执行命令。

## <a name="beforepackage"></a>BeforePackage
 `BeforePackage`元素指示安装程序来安装指定的包之前执行命令。

## <a name="afterpackage"></a>AfterPackage
 `AfterPackage`元素指示要执行的命令之后安装指定的包, 的安装程序。

## <a name="see-also"></a>请参阅
- [\<产品 > 元素](../deployment/product-element-bootstrapper.md)
- [产品和包架构引用](../deployment/product-and-package-schema-reference.md)