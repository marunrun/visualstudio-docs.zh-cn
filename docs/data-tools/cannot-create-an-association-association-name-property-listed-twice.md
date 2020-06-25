---
title: 无法创建关联 - 属性被列出了两次
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 3ced8bda-210e-4caf-9d8f-96cdbba19251
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 92999e211ec0f7265f026446e09dbc94cc3060f3
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282795"
---
# <a name="cannot-create-an-association-ltassociation-namegt---property-listed-twice"></a>无法创建关联 &lt;关联名称&gt; - 属性已列出两次

无法创建关联 \<association name> 。 多次列出相同的属性： \<property name> 。

关联由在“关联编辑器”对话框中选择的“关联属性”定义********。 对于关联中的每个类，属性只能列出一次。

消息中的属性在 Parent 类或 Child 类的“关联属性”中出现了多次****。

## <a name="to-resolve-this-condition"></a>解决此问题的方法

- 检查消息并记下消息中指定的属性。

- 单击“确定”，关闭该消息框****。

- 检查“关联属性”并移除重复项****。

- 单击 **“确定”** 。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [如何：在 LINQ to SQL 类之间创建关联（O/R 设计器）](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md)