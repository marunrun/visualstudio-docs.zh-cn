---
title: 使用类设计器
ms.date: 05/08/2018
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.diagram
helpviewer_keywords:
- Class Designer [Visual Studio]
- Class Designer, about Class Designer
- types [Visual Studio], viewing
- classes [Visual Studio], viewing
- class designer
ms.assetid: 40ed2c9d-0ce0-4b95-ad78-5dec2065ccea
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ee4910471693a2941ec9548773a2f50e443a639b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62975560"
---
# <a name="design-and-view-classes-and-types-with-class-designer"></a>使用类设计器设计和查看类和类型

使用 Visual Studio 中的类设计器设计、直观显示和重构代码中的类和其他类型。 使用类图来创建和编辑 C#、Visual Basic 或 C++ 项目中的类。 也可以使用类图深入了解项目结构或重新组织代码。

## <a name="what-you-can-do-with-class-diagrams"></a>如何使用类图

- **设计**：通过编辑类图来编辑项目代码。 添加新元素和删除不需要的元素。 所做的更改将反映在代码中。

- **可视化**：通过在图上查看项目中的类来了解项目结构。 自定义图表，以便将重点放在你最关注的项目详细信息上。 保存图表以供将来演示或存档使用。

- **重构**：重写方法、重命名标识符、重构参数和实现接口和抽象类。

## <a name="view-types-and-relationships"></a>查看类型和关系

类图显示类型详细信息，例如，它们的构成成员及这些成员之间的关系。 这些实体的可视化是代码中的动态视图。 这意味着可以在设计器中编辑类型，然后查看反射在实体源代码中的编辑内容。 同样，类图将与对代码文件所做的更改保持同步。

> [!NOTE]
> 如果项目包含类图，并且项目引用了另一个项目中的类型，则在为该类型生成项目前，类图不会显示该引用的类型。 同样，在为该实体重新生成项目前，该类图不会显示对外部实体代码所做的更改。

## <a name="class-diagram-workflow"></a>类图工作流

可通过类图了解项目的类结构。 这些项目可能已由其他开发人员创建，或者可以对自己创建的某个项目作一些改变。 可以使用类图来自定义、共享并向其他人展示项目信息。

展示项目信息的第一步是创建一个可显示要展示的内容的类图。 有关详细信息，请参阅[添加类图](how-to-add-class-diagrams-to-projects.md)。 你可以为项目创建多个类图，可用于显示项目的不同视图、选定的项目类型子集或选定的类型成员子集。

除了定义类图显示的内容，还可以更改信息的呈现方式的；有关详细信息，请参阅[如何：自定义类图](how-to-customize-class-diagrams.md)。

在对一个或多个类图进行微调之后，你可以将它们复制到 Microsoft Office 文档中并打印出来，或是将它们作为图像文件导出。 有关详细信息，请参阅[如何：将类图元素复制到 Microsoft Office 文档](how-to-copy-class-diagram-elements-to-a-microsoft-office-document.md)、[如何：打印类图](how-to-print-class-diagrams.md)以及[如何：将类图作为图像导出](how-to-export-class-diagrams-as-images.md)。

> [!NOTE]
> 类设计器不会跟踪源文件的位置，因此更改项目结构或移动项目中的源文件就可能导致类设计器无法继续对类型进行跟踪，尤其是 typedef 的源类型、基类或关联类型。 可能会收到错误，如“类设计器无法显示此类型”。 如果收到错误，要将修改过的或被重新定位的源代码再次拖到类图中以重新显示。

## <a name="see-also"></a>请参阅

- [代码编辑器功能](../writing-code-in-the-code-and-text-editor.md)
- [映射解决方案中的依赖项](../../modeling/map-dependencies-across-your-solutions.md)