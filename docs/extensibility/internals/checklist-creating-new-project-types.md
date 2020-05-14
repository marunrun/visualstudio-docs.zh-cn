---
title: 清单：创建新的项目类型 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating new types
- project types, checklist for creating
ms.assetid: 29eb9c3b-1933-4741-aa85-65a33f0825ba
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5963083239571af43012e1a79576ee80846d80bd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709751"
---
# <a name="checklist-create-new-project-types"></a>检查表：创建新的项目类型
您必须完成多个任务才能创建新的项目类型。 以下检查表提供了这些任务的指南：

1. 设计新项目类型的功能。 有关详细信息，请参阅[项目类型设计决策](../../extensibility/internals/project-type-design-decisions.md)。

2. 确定哪些编辑器用于代码和其他项目元素。 您可以使用核心编辑器或标准编辑器，也可以创建和使用特定于项目的编辑器。 有关详细信息，请参阅[创建自定义编辑器和设计器](../../extensibility/creating-custom-editors-and-designers.md)[以及如何：打开特定于项目的编辑器](../../extensibility/how-to-open-project-specific-editors.md)。

3. 确定项目项目在**类视图**和**对象浏览器**中的参与程度。 有关详细信息，请参阅[支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)。

4. 基于您以前为项目和项目项目项目所做的设计决策派生新类。

5. 为以下项目类型组件编写代码：

    - 项目工厂，管理创建新项目和打开现有项目。 有关详细信息，请参阅[使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)。

    - 项目层次结构和命令处理。 有关详细信息，请参阅使用[HierUtil7 项目类来实现项目类型（C++）、](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)[项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)、[项目模型核心组件](../../extensibility/internals/project-model-core-components.md)以及[MenuCommands 与 OleMenuCommands](/visualstudio/extensibility/menucommands-vs-olemenucommands?view=vs-2015)。

    - 项目项目管理，包括将项目添加到 **"新项目**"对话框。 有关详细信息，请参阅[添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)以及[注册项目和项目模板](../../extensibility/internals/registering-project-and-item-templates.md)。

    - 项目状态和单个项的持久性。 有关详细信息，请参阅[打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)。 有关解决方案信息的持久性，请参阅[解决方案](../../extensibility/internals/solutions-overview.md)。

    - 要在"属性"窗口中显示与配置无关的属性。 有关详细信息，请参阅[扩展属性](../../extensibility/internals/extending-properties.md)。

    - 在属性页中实现的项目配置属性以显示与配置相关的属性。 有关详细信息，请参阅[管理配置选项](../../extensibility/internals/managing-configuration-options.md)。

    - 枚举部署的输出。 有关详细信息，请参阅[输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)。

    - 项目启动服务。 有关详细信息，请参阅[项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)和[项目模型核心组件](../../extensibility/internals/project-model-core-components.md)。

    - 对象或派生自`IDispatch`的类可用于自动化。

    - XML 命令表 （*.vsct*） 文件。 有关详细信息，请参阅[可视化工作室命令表 （.vsct） 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

6. 测试、调试和启动项目类型。

7. 通过将`VARIANT_TRUE`设置为`VSHPROPID_ShowProjInSolutionPage`的值，在 **"添加参考"** 对话框的"**项目**"选项卡中显示项目。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>。

8. 创建用于安装 VS 包的 Microsoft 安装程序 （*.msi*） 文件。 有关详细信息，请参阅使用[Windows 安装程序安装 VS 包](../../extensibility/internals/installing-vspackages-with-windows-installer.md)、[注册项目类型](../../extensibility/internals/registering-a-project-type.md)和[VS 包](../../extensibility/internals/vspackages.md)。

## <a name="see-also"></a>请参阅
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [何时创建项目类型](../../extensibility/internals/when-to-create-project-types.md)
- [创建项目类型](../../extensibility/internals/creating-project-types.md)
