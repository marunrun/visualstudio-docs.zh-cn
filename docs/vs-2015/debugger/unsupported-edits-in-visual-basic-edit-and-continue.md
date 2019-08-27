---
title: 编辑并继续在 Visual Basic 中的不支持的编辑 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
helpviewer_keywords:
- Edit and Continue [Visual Basic], unsupported method and property body edits
ms.assetid: 9b8fdc41-a193-49ad-ad72-dfcadd46f4b3
caps.latest.revision: 31
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 94a151a7adab5c8246cec38c2e62d76788beb6e7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155438"
---
# <a name="unsupported-edits-in-visual-basic-edit-and-continue"></a>Visual Basic“编辑并继续”中不支持的编辑
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

利用“编辑并继续”，您可以在中断模式下停止程序执行，对执行代码进行更改，以及继续执行包含新更改的程序。 通常情况下，影响类的公共结构的声明性代码编辑是禁止的，但对类内部的方法、属性体或私有声明的很多编辑是允许的。  
  
 如果需要进行不受支持的更改，则必须停止调试，执行更改，然后启动新的调试会话。  
  
### <a name="BKMK_MethodandPropertyBodyEdits"></a> 方法和属性体编辑  
 **不受支持的更改对静态局部变量**:添加或更新本地变量，或如果该删除静态局部变量将导致编译错误。  
  
 **不支持对泛型的更改**:对泛型方法本身和泛型方法体的更改不受支持。 可以添加、删除或更改泛型类型的实例化或对现有泛型方法的调用。  
  
 **其他不受支持的更改**  
  
- 更改调用堆栈中的方法的调用语句。  
  
- 当指令指针结束于 `Try...Catch` 块或 `Catch` 块中时，添加 `Finally` 块。  
  
- 删除`Try...Catch`块中，当指令指针位于`Catch`块或`Finally`块。  
  
- 在当前指令指针的前后添加 `Using` 块。  
  
- 在当前指令指针的前后添加 `SynchLock` 块。  
  
### <a name="BKMK_AttributeEdits"></a> 特性编辑  
 “编辑并继续”不支持修改特性。 具体而言，“编辑并继续”不支持以下更改：  
  
- 定义、编辑或删除特性类。  
  
- 添加特性。  
  
- 编辑或移除现有特性。  
  
### <a name="BKMK_ClassDeclarationEdits"></a> 类声明编辑  
 当在中断模式下时，“编辑并继续”不允许对类声明的大多数更改。 具体而言，“编辑并继续”不支持以下更改：  
  
- 重命名、删除或更改现有类的继承。  
  
- 实现新接口或移除接口的实现。  
  
- 针对类更改修饰符。  
  
- 添加、更改或移除 `ComClass` 状态。  
  
- 编辑任何泛型类声明。  
  
### <a name="BKMK_ClassMemberDeclarationEdits"></a> 类成员声明编辑  
 大多数“编辑并继续”情况中都禁止对成员声明的更改。 例如，如果此更改会导致编译错误，则不能更改成员的签名或访问级别，并且不能完全删除成员。 具体而言，“编辑并继续”不支持以下更改：  
  
- 通过在包含块中声明具有相同名称的全局或成员变量来隐藏现有成员变量。  
  
- 通过在块内声明新实例来隐藏静态局部变量。  
  
- 移除事件的处理程序。 允许添加事件处理程序。  
  
- 添加新的重载属性或方法，除非该属性或方法是 `Private` 的并且任何活动语句中均未出现其名称。  
  
- 添加或移除成员变量上的 `WithEvents` 子句。  
  
- 删除成员。  
  
- 更改属性或方法声明以停止实现接口。  
  
- 编辑使用泛型的任何方法。  
  
- 更改签名或返回非私有属性或方法的类型。  
  
- 在基类中重写或隐藏成员。  
  
- 在标记为 `SequentialLayout` 或 `ExplicitLayout` 的任何类中添加新的字段。  
  
- 更改方法的 `MustInherit` 或 `NotOverridable` 状态。  
  
- 更改属性或方法的访问修饰符。  
  
- 更改字段的类型或只读状态。  
  
- 更改公共字段。  
  
### <a name="BKMK_CompilerOptionEdits"></a> 编译器选项编辑  
 当在中断模式下使用“编辑并继续”时，不能更改、添加或移除以下编译器选项：  
  
- Option Strict   
  
- Option Explicit   
  
- Option Compare   
  
### <a name="BKMK_ConstantsEdits"></a> 常量编辑  
 当在“编辑并继续”模式下时，对常量的更改非常受限制。 具体而言，“编辑并继续”不支持以下更改：  
  
- 添加或更新常量变量。  
  
- 更改常量的类型或值。  
  
- 移除常量。  
  
### <a name="BKMK_DelegateandEventDeclarationEdits"></a> 委托和事件声明编辑  
 在中断模式下，“编辑并继续”不允许对委托和事件的某些更改。 具体而言，“编辑并继续”不支持以下更改：  
  
- 更改或删除委托定义。  
  
- 删除事件。  
  
### <a name="BKMK_EnumerationEdits"></a> 枚举编辑  
 在中断模式期间，“编辑并继续”不允许对枚举 (`Enums`) 进行更改。 具体而言，“编辑并继续”不支持以下更改：  
  
- 修改 `Enum` 的基础类型。  
  
- 添加、更改或移除 `Enum` 成员。  
  
- 更改 `Enum` 的访问修饰符。  
  
### <a name="BKMK_ExternalDeclarationsEdits"></a> 外部声明编辑  
 一般来说，在“编辑并继续”过程中，您不能更改外部方法的声明。 具体而言，“编辑并继续”不支持以下更改：  
  
- 添加或移除外部声明。  
  
- 更改外部声明的签名或封送外部声明的特性。  
  
### <a name="BKMK_ImportsEdits"></a> 导入编辑  
 当在中断模式下时，“编辑并继续”不允许添加、更改或移除 `Imports` 语句。  
  
### <a name="BKMK_InterfaceDefinitionEdits"></a> 接口定义编辑  
 尽管您经常可以更改实现接口的成员，但“编辑并继续”通常不允许更改实际接口定义。 具体而言，“编辑并继续”不支持以下更改：  
  
- 添加、更改或移除接口成员。  
  
- 删除现有接口。  
  
- 更改接口的访问修饰符。  
  
- 更改接口继承层次结构。  
  
### <a name="BKMK_ModuleDeclarationEdits"></a> 模块声明编辑  
 当在中断模式下时，“编辑并继续”不允许对模块声明的大多数更改。 具体而言，“编辑并继续”不支持以下更改：  
  
- 创建新模块。  
  
- 重命名或删除现有模块。  
  
- 更改模块的访问修饰符。  
  
### <a name="BKMK_ModuleMemberDeclarationEdits"></a> 模块成员声明编辑  
 利用“编辑并继续”，您可以在中断模式下对模块成员（如属性、方法和字段）进行各种更改。 但是，不支持某些更改。 最值得注意的是，“编辑并继续”不支持添加、删除或更改任何成员的类型或签名。  
  
 具体而言，“编辑并继续”不支持以下更改：  
  
- 添加新成员，除非任何活动语句中均未出现该名称。  
  
- 移除属性或方法。  
  
- 更改属性或方法的签名。  
  
- 添加、重命名、移动或删除字段。  
  
- 编辑使用泛型的任何方法。  
  
- 更改属性或方法的访问修饰符（例如，将 `Public` 更改为 `Private`）。  
  
- 删除或更改现有字段的类型。  
  
### <a name="BKMK_NestedTypeDeclarationEdits"></a> 嵌套的类型声明编辑  
 “编辑并继续”不支持将嵌套类型移动到另一个命名空间或类型。  
  
### <a name="BKMK_StructureDeclarationEdits"></a> 结构声明编辑  
 通过在编辑并继续时不允许对结构声明的大多数更改**中断**模式。 具体而言，“编辑并继续”不支持以下更改：  
  
- 重命名或删除现有结构。  
  
- 实现新接口或移除接口的实现。  
  
- 更改结构的访问修饰符。  
  
### <a name="BKMK_StructureMemberDeclarationEdits"></a> 结构成员声明编辑  
 利用“编辑并继续”，您可以在中断模式下对结构成员（如属性、方法和字段）进行各种更改。 但是，有些更改不受支持，特别是影响结构成员的声明的更改。 具体而言，“编辑并继续”不支持以下更改：  
  
- 移除属性或方法。  
  
- 添加或移除字段。  
  
- 更改属性或方法的签名。  
  
- 编辑使用泛型的任何方法。  
  
- 更改属性或方法声明是否实现接口。  
  
- 更改属性或方法的访问修饰符 (例如，更改`Public`到**专用**)。  
  
- 移除字段。  
  
- 更改字段的类型。  
  
## <a name="see-also"></a>请参阅  
 [如何：应用编辑在中断模式下使用编辑并继续](../debugger/how-to-apply-edits-in-break-mode-with-edit-and-continue.md)   
 [编辑并继续 (Visual Basic)](../debugger/edit-and-continue-visual-basic.md)
