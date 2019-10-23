---
title: 如何：在元素上设置 CLR 特性
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f943f9713e4432f0b06242a2f66acae6b390e5cc
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748367"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>如何：在元素上设置 CLR 特性
自定义属性是可以添加到域元素、形状、连接符和关系图中的特殊属性。 可以添加从 `System.Attribute` 类继承的任何属性。

### <a name="to-add-a-custom-attribute"></a>添加自定义属性

1. 在 " **DSL 资源管理器**" 中，选择要向其添加自定义属性的元素。

2. 在 "**属性**" 窗口中，在 "**自定义属性**" 属性旁边，单击 "浏览（ **...** ）" 图标。

     此时将打开 "**编辑属性**" 对话框。

3. 在 "**名称**" 列中，单击 " **\<add 属性" >** 并键入属性的名称。 按 Enter。

4. 属性名称下面的行显示括号。 在此行上，键入属性的参数类型（例如 `string`），然后按 ENTER。

5. 在 "**名称属性**" 列中，键入适当的名称，例如 `MyString`。

6. 单击“确定”。

     "**自定义属性**" 属性现在按以下格式显示属性：

     `[` *AttributeName* `(` *ParameterName* `=`*类型*`)]`

## <a name="see-also"></a>请参阅

- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)