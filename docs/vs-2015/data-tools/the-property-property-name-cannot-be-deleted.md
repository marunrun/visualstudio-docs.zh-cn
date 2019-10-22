---
title: 无法删除 &lt;property 名称 &gt; 的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 55873f74-7834-4ec1-8815-eeeb65618d87
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: aca36919cb4c82d6ca76e0f3eecbbacd48cde768
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667238"
---
# <a name="the-property-ltproperty-namegt-cannot-be-deleted"></a>无法删除属性 &lt;property 名称 &gt;
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

无法删除属性 \<property 名称 >，因为它被设置为 \<class 名称 > 和 \<class 名称之间的继承的鉴别器属性 >

 选择的属性被设置为“鉴别器属性”，用于错误消息中所指示的类之间的继承。 如果属性参与数据类之间的继承配置，则无法删除这些属性。

 将“鉴别器属性”设置为数据类的另一个属性，可以成功删除希望删除的属性。

### <a name="to-correct-this-error"></a>更正此错误

1. 在 O/R 设计器中选择连接错误消息中指示的数据类的继承连线。

2. 将“鉴别器”属性设置为另一个属性。

3. 再次尝试删除该属性。

## <a name="see-also"></a>请参阅
 [如何：使用 O/R 设计器](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)[数据类继承配置继承（o/r 设计器）](../data-tools/data-class-inheritance-o-r-designer.md) [演练：通过使用单表继承创建 LINQ to SQL 类（O/r 设计器）](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)
