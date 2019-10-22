---
title: 搜索表达式中的逻辑运算符 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Help Viewer 2.0, logical operators in search
- logical operators in search [Help Viewer 2.0]
ms.assetid: 0c38ae7d-3e20-4d47-a020-9677cd285916
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3d56f2dfc2924008a6be293fe1498f0ffe32abaf
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651431"
---
# <a name="logical-operators-in-search-expressions"></a>搜索表达式中的逻辑运算符
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过使用逻辑运算符，可以在较简单的表达式基础上创建更复杂的搜索表达式，以改进内容的搜索。 如下表所示，逻辑运算符指定在搜索查询中组合多个搜索词的方式。

> [!IMPORTANT]
> 必须使用全部大写字母的格式输入逻辑运算符，以便搜索引擎可以识别它们。

|要搜索|使用|示例|结果|
|-------------------|---------|-------------|------------|
|同一主题中的两个词|AND|dib AND palette|包含“dib”和“palette”的主题。|
|主题中的任一个词|或|raster OR vector|包含“raster”或“vector”的主题|
|同一主题中包含第一个词，而不包含第二个词|NOT|"operating system" NOT DOS|包含“operating system”但不包含“DOS”的主题。|
|主题中两个词相互靠近|相邻|user NEAR kernel|包含与“kernel”靠近的“user”的主题。|

## <a name="see-also"></a>另请参阅
 [全文搜索提示](../ide/full-text-search-tips.md)[查找信息](../ide/locate-information.md)
