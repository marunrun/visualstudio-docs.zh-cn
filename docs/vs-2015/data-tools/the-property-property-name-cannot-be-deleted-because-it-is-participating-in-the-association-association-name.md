---
title: 无法删除属性 &lt;property 名称 &gt;，因为它参与了关联 &lt;association 名称 &gt; |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 389873cc-92dd-48da-bfca-0f6c8e0ae3c2
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 53bf12a84a705ddca0cacffc36028698cb08443a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667272"
---
# <a name="the-property-ltproperty-namegt-cannot-be-deleted-because-it-is-participating-in-the-association-ltassociation-namegt"></a>无法删除属性 &lt;属性名称&gt;，原因是它参与了关联 &lt;关联名称&gt;
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

选择的属性被设置为错误消息中指示的类之间关联的“关联属性”。 如果属性参与了数据类之间的关联，则无法删除。

 将“关联属性”设置为数据类的另一个属性，可以成功删除希望删除的属性。

### <a name="to-correct-this-error"></a>更正此错误

1. 在 O/R 设计器中选择连接错误消息中指示的数据类的关联连线。

2. 双击该连线以打开“关联编辑器”对话框。

3. 从“关联属性”中移除该属性。

4. 再次尝试删除该属性。

## <a name="see-also"></a>请参阅
 [LINQ to SQL Visual Studio 中的工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)[如何：在 LINQ to SQL 类之间创建关联（关系）（o/R 设计器）](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md) [演练：创建 LINQ to SQL 类（o-r 设计器）](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)
