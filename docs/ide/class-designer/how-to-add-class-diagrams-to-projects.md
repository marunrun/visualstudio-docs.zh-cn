---
title: 如何：向项目中添加类图（类设计器）
ms.date: 05/08/2018
ms.topic: how-to
helpviewer_keywords:
- class diagrams, creating
- Class Designer [Visual Studio], opening
ms.assetid: 0eac1b54-2711-4e4b-9654-a0c429c08c8f
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a54b01f718c2faab8d36cc8e44805707fd0cc35f
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771033"
---
# <a name="how-to-add-class-diagrams-to-projects"></a>如何：向项目添加类图

若要设计、编辑及重构类和其他类型，请将类图添加到 C#、Visual Basic 或 C++ 项目中。 若要直观显示项目中代码的不同部分，请将多个类图添加到该项目中。

你不可以从在多个应用间共享代码的项目创建类图。 要创建 UML 类图，请参阅[创建 UML 建模项目和关系图](../../modeling/what-s-new-for-design-in-visual-studio.md)。

## <a name="install-the-class-designer-component"></a>安装类设计器组件

如果尚未安装“类设计器”组件，请按照以下步骤进行安装  。

1. 从 Windows 开始菜单中，或通过从 Visual Studio 中的菜单栏中选择“工具” > “获取工具和功能”，打开“Visual Studio 安装程序”。

   “Visual Studio 安装程序”  随即打开。

1. 选择“单个组件”  选项卡，然后向下滚动到“代码工具”  类别。

1. 选择“类设计器”  ，然后选择“修改”  。

   ![Visual Studio 安装程序中的类设计器组件](media/class-designer-component.png)

   “类设计器”  组件开始安装。

## <a name="add-a-blank-class-diagram-to-a-project"></a>向项目中添加空白类图

1. 在“解决方案资源管理器”  中，右键单击项目节点，并选择“添加”   > “新项”  。 或按 Ctrl+Shift+A。

   “添加新项”  对话框随即打开。

2. 展开“常用项”   > “常规”  ，然后从模板列表中选择“类图”  。 对于 Visual C++ 项目，查看“实用工具”  类别并查找“类图”  模板。

   > [!NOTE]
   > 如果未看到“类图”  模板，[按步骤](#install-the-class-designer-component)安装适用于 Visual Studio 的“类设计器”  组件。

   类图随即在类设计器中打开，并在“解决方案资源管理器”中以一个带 .cd 扩展名的文件出现。 可以将形状和线条从“工具箱”  拖动至关系图。

要添加多个类图，请重复上述步骤。

## <a name="add-a-class-diagram-based-on-existing-types"></a>基于现有类型添加类图

在“解决方案资源管理器”  中，打开类文件上下文菜单（右键单击），然后选择“查看类图”  。

或

在“类视图”  中，打开命名空间或类型上下文菜单，然后选择“查看类图”  。

> [!TIP]
> 如果类视图尚未打开，则从“视图”菜单打开类视图    。

## <a name="to-display-the-contents-of-a-complete-project-in-a-class-diagram"></a>在类图中显示完整项目的内容

在“解决方案资源管理器”或“类视图”中，右键单击该项目并选择“视图”，然后选择“查看类图”    。

即会创建一个自动填充的类图。

> [!NOTE]
> 类设计器在 .NET Core 项目中不可用。

## <a name="see-also"></a>另请参阅

- [如何：使用类设计器创建类型](how-to-create-types.md)
- [如何：查看现有类型](how-to-view-existing-types.md)
- [设计和查看类和类型](designing-and-viewing-classes-and-types.md)
