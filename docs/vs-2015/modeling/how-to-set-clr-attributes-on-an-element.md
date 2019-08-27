---
title: 如何：在元素上设置 CLR 特性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
ms.assetid: b3db3c74-920c-4701-9544-6f75cbe8b7c9
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f9af25934a40c01c6b4cfd48dcd7419bddf322d3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65698025"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>如何：在元素上设置 CLR 属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

自定义属性是特殊属性，可以添加到域元素、 形状、 连接符和关系图。 您可以添加任何属性继承自`System.Attribute`类。  
  
### <a name="to-add-a-custom-attribute"></a>若要添加的自定义属性  
  
1. 在中**DSL 资源管理器**，选择你想要添加的自定义属性的元素。  
  
2. 在中**属性**窗口中，为下的一步**自定义特性**属性中，单击浏览 ( **...** ) 图标。  
  
     **编辑属性**对话框随即打开。  
  
3. 在中**名称**列中，单击 **\<添加属性>** 键入属性的名称。 按 Enter。  
  
4. 在属性名称下的行显示括号。 在这行上键入该属性的参数类型 (例如， `string`)，然后按 ENTER。  
  
5. 在中**名称属性**列中，键入相应的名称，例如， `MyString`。  
  
6. 单击 **“确定”** 。  
  
     **自定义特性**属性现在显示的属性采用以下格式：  
  
     `[` *AttributeName* `(` *ParameterName* `=` *Type* `)]`  
  
## <a name="see-also"></a>请参阅  
 [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
