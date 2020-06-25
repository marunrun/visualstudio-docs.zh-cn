---
title: 无法删除属性
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 55873f74-7834-4ec1-8815-eeeb65618d87
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 91fce94babf443c974a49885263b8e7eb77d9eaa
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281340"
---
# <a name="the-property-property-name-cannot-be-deleted"></a>属性 \<property name> 无法删除

\<property name>无法删除属性，因为它被设置为与之间的继承的**鉴别**器属性 \<class name>\<class name>

选择的属性被设置为“鉴别器属性”，用于错误消息中所指示的类之间的继承****。 如果属性参与数据类之间的继承配置，则无法删除这些属性。

将“鉴别器属性”设置为数据类的另一个属性，可以成功删除希望删除的属性****。

## <a name="to-correct-this-error"></a>更正此错误

1. 在**O/R 设计器**中，选择连接错误消息中指示的数据类的继承连线。

2. 将“鉴别器”属性设置为另一个属性****。

3. 再次尝试删除该属性。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)