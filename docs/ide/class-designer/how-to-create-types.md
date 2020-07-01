---
title: 如何：使用类设计器创建类型
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- VS.Clr.ClrAttributesDialog
helpviewer_keywords:
- custom attributes, applying
- class diagrams, creating types
- classes [Visual Studio], creating with Class Designer
- Class Designer [Visual Studio], creating classes
- types [Visual Studio], class diagrams
- attributes [Visual Studio], applying custom
ms.assetid: 94458c31-28bc-40e2-9737-85868788a0e5
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 98e489a37e5d75cbc17d17c32a1fa3b53f9993f8
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770218"
---
# <a name="how-to-create-types-by-using-class-designer"></a>如何：使用类设计器创建类型

若要设计 C# 和 Visual Basic 项目的新类型，请在类图上创建它们。 若要查看现有类型，请参阅[如何：查看现有类型](how-to-view-existing-types.md)。

## <a name="create-a-new-type"></a><a name="CreateType"></a>创建新类型

1. 在“工具箱”的“类设计器”下，将以下之一拖动到类图上   ：

    - “类”或“抽象类”  

    - **Enum**

    - **Interface**

    - “结构”(VB) 或“结构”(C#)  

    - **Delegate**

    - “模块”（仅限 VB） 

2. 为该类型命名。 然后选择其访问级别。

3. 选择要在其中添加该类型的初始代码的文件：

    - 若要创建新文件并将其添加到当前项目，请选择“创建新文件”，并为该文件命名  。

    - 若要将代码添加到现有文件，请选择“添加到现有文件”  。

         如果你的解决方案有共享跨多个应用的代码的项目，你可以将新类型添加到应用项目中的类图，但前提是相应的类文件在同一应用项目中或共享项目中。

4. 现在添加其他项以定义该类型：

    |**对于**|**添加**|
    |-|-|
    |类、抽象类、结构|定义类型的方法、属性、字段、事件、构造函数（方法）、析构函数（方法）和常量|
    |枚举|组成枚举的字段值|
    |接口|组成接口的方法、属性和事件|
    |委托|定义委托的参数|
    |模块|定义模块的方法、属性、字段、事件、构造函数（方法）和常量|

     请参阅[创建成员](creating-and-configuring-type-members.md#create-members)。

## <a name="apply-a-custom-attribute-to-a-type"></a><a name="CustAttributeType"></a>将自定义特性应用于类型

1. 在类图上单击类型的形状。

2. 在“属性”中，单击类型的“自定义属性”属性旁边的省略号 (...) 按钮   。

3. 添加一个或多个自定义特性，一行一个。 请不要将它们放在括号内。

   自定义属性随即应用于类型。

## <a name="apply-a-custom-attribute-to-a-type-member"></a><a name="CustAttributeMember"></a>将自定义特性应用于类型成员

1. 在类图上类型的形状中单击成员的名称，或者在“类详细信息”窗口中单击成员所在的行。

2. 在“属性”中，查找成员的“自定义属性”属性   。

3. 添加一个或多个自定义特性，一行一个。 请不要将它们放在括号内。

   自定义属性随即应用于类型。

## <a name="see-also"></a>另请参阅

- [如何：创建类型之间的继承](how-to-create-inheritance-between-types.md)
- [如何：创建类型之间的关联](how-to-create-associations-between-types.md)
- [创建和配置类型成员](creating-and-configuring-type-members.md)
- [设计类和类型](designing-and-viewing-classes-and-types.md)
