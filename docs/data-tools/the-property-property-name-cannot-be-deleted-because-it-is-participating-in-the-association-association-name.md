---
title: 属性参与关联
description: 无法删除属性，因为该属性正在参与关联
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 389873cc-92dd-48da-bfca-0f6c8e0ae3c2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: ead87955056ec3c6246df6fc9050eedd867dd3ef
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89743283"
---
# <a name="the-property-ltproperty-namegt-cannot-be-deleted-because-it-is-participating-in-the-association-ltassociation-namegt"></a>无法删除属性 &lt;属性名称&gt;，原因是它参与了关联 &lt;关联名称&gt;

选择的属性被设置为错误消息中指示的类之间关联的“关联属性”****。 如果属性参与了数据类之间的关联，则无法删除。

将“关联属性”设置为数据类的另一个属性，可以成功删除希望删除的属性****。

## <a name="to-correct-this-error"></a>更正此错误

1. 在连接错误消息中指示的数据类的 **O/R 设计器** 上选择关联连线。

2. 双击该连线以打开“关联编辑器”对话框****。

3. 从“关联属性”中移除该属性****。

4. 再次尝试删除该属性。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)