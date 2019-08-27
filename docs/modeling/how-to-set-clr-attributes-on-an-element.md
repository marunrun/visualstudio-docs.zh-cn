---
title: 如何：在元素上设置 CLR 属性
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8954aa6a42e743617080bb6918508273c1dd9528
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62811272"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>如何：在元素上设置 CLR 属性
自定义属性是特殊属性，可以添加到域元素、 形状、 连接符和关系图。 您可以添加任何属性继承自`System.Attribute`类。

### <a name="to-add-a-custom-attribute"></a>若要添加的自定义属性

1. 在中**DSL 资源管理器**，选择你想要添加的自定义属性的元素。

2. 在中**属性**窗口中，为下的一步**自定义特性**属性中，单击浏览 ( **...** ) 图标。

     **编辑属性**对话框随即打开。

3. 在中**名称**列中，单击 **\<添加属性 >** 键入属性的名称。 按 Enter。

4. 在属性名称下的行显示括号。 在这行上键入该属性的参数类型 (例如， `string`)，然后按 ENTER。

5. 在中**名称属性**列中，键入相应的名称，例如， `MyString`。

6. 单击 **“确定”** 。

     **自定义特性**属性现在显示的属性采用以下格式：

     `[` *AttributeName* `(` *ParameterName* `=` *Type* `)]`

## <a name="see-also"></a>请参阅

- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)