---
title: 无法删除属性
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 55873f74-7834-4ec1-8815-eeeb65618d87
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: c03ba87a7ae7f2321550179ae6354eb473c81465
ms.sourcegitcommit: 50f0c3f2763a05de8482b3579026d9c76c0e226c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65460561"
---
# <a name="the-property-property-name-cannot-be-deleted"></a>无法删除属性 \<属性名称>

无法删除属性 \<属性名称>，因为它被设置为用于 \<类名称> 和 \<类名称> 之间的继承的鉴别器属性

选择的属性被设置为“鉴别器属性”，用于错误消息中所指示的类之间的继承。 如果属性参与数据类之间的继承配置，则无法删除这些属性。

将“鉴别器属性”设置为数据类的另一个属性，可以成功删除希望删除的属性。

## <a name="to-correct-this-error"></a>更正此错误

1. 在 O/R 设计器中选择连接错误消息中指示的数据类的继承连线。

2. 将“鉴别器”属性设置为另一个属性。

3. 再次尝试删除该属性。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)