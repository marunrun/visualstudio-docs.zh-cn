---
title: XML 架构
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.xmleditor.schemasdialog
ms.assetid: 0271fa26-2205-49bd-96e0-ae1441571808
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d01c56b04a9b046f695a19d61a9b47fcac73e06
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592329"
---
# <a name="xml-schemas-dialog-box"></a>XML 架构对话框

“XML 架构”对话框用于选择要与 XML 文档关联的 XML 架构定义语言 (XSD) 架构。 您可以从架构缓存中选择架构，也可以指定不在缓存中的架构。 选定的架构被视为架构集的一部分。 架构集用于 IntelliSense 和 XML 文档验证。

通过单击文档属性窗口上的“架构”按钮，或从“XML”菜单上选择“架构”，可以访问“XML 架构”对话框   。

## <a name="uielement-list"></a>UIElement 列表

**使用**

选择如何使用“XML 架构”。

- **自动**。 当前文档未使用此架构，但是此架构可用于自动关联。 如果 XML 文档声明一个与此架构的 `targetNamespace` 匹配的命名空间，则将自动关联此架构并将其包含在架构集中。

- 使用此架构。 当前文档正在使用此架构。 用户已显式请求通过单击此列来使用此架构，或者根据匹配的 `targetNamespace` 自动关联此架构。

- 不使用所选架构。 当前文档不使用此架构，即使此架构具有匹配的 `targetNamespace`。 当架构缓存或解决方案中有同一架构的多个版本时，可以使用此设置来解决冲突。

目标命名空间

显示与 XML 架构关联的目标命名空间。

**文件名**

显示 XML 架构文件名。

**添加**

打开“打开 XSD 架构”对话框，使用此对话框可以选择要添加到架构集的其他架构。 将架构添加到架构集时，“使用”列的值设置为“使用此架构” 。

**移除**

从架构集中移除当前所选的架构。 该操作将从内存中的架构缓存中移除架构，但不从文件系统中移除架构。

## <a name="see-also"></a>请参阅

- [如何：选择要使用的 XML 架构](../xml-tools/how-to-select-the-xml-schemas-to-use.md)
- [架构缓存](../xml-tools/schema-cache.md)
