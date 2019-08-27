---
title: 清单：创建新的项目类型 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating new types
- project types, checklist for creating
ms.assetid: 29eb9c3b-1933-4741-aa85-65a33f0825ba
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 64e00c452f01c95046b4dc669dbd3bdd1517d287
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309193"
---
# <a name="checklist-create-new-project-types"></a>清单：创建新的项目类型
必须完成多个任务以创建新的项目类型。 下列清单提供了这些任务的指南：

1. 设计新的项目类型的功能。 有关详细信息，请参阅[项目类型设计决策](../../extensibility/internals/project-type-design-decisions.md)。

2. 确定将哪个编辑器用于代码和其他项目元素。 可以使用的核心或标准编辑器，也可以创建和使用特定于项目的编辑器。 有关详细信息，请参阅[创建自定义编辑器和设计器](../../extensibility/creating-custom-editors-and-designers.md)和[如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)。

3. 确定项目项都将具有中的参与等级**类视图**并**对象浏览器**。 有关详细信息，请参阅[支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)。

4. 派生新类根据先前创建的项目和项目项的设计决策。

5. 编写以下项目类型组件的代码：

    - 项目工厂，来管理创建新项目和打开现有项目。 有关详细信息，请参阅[使用项目工厂创建的项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)。

    - 项目层次结构和命令处理。 有关详细信息，请参阅[使用 HierUtil7 项目类以实现一种项目类型 (C++)](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)，[项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)，[项目模型核心组件](../../extensibility/internals/project-model-core-components.md)，并[MenuCommands 与。OleMenuCommands](../../extensibility/menucommands-vs-olemenucommands.md)。

    - 项目项管理，包括添加到项目**新的项目**对话框。 有关详细信息，请参阅[添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)并[注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)。

    - 暂留的项目状态和各个项。 有关详细信息，请参阅[打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)。 有关持久性的解决方案的信息，请参阅[解决方案](../../extensibility/internals/solutions-overview.md)。

    - 若要在属性窗口中显示的独立于配置的属性。 有关详细信息，请参阅[扩展属性](../../extensibility/internals/extending-properties.md)。

    - 在属性页以显示依赖于配置的属性中实现的项目配置属性。 有关详细信息，请参阅[管理的配置选项](../../extensibility/internals/managing-configuration-options.md)。

    - 枚举用于部署的输出。 有关详细信息，请参阅[输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)。

    - 项目启动服务。 有关详细信息，请参阅[项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)并[项目模型核心组件](../../extensibility/internals/project-model-core-components.md)。

    - 对象或从派生的类`IDispatch`，可用于自动化。

    - XML 命令表 ( *.vsct*) 文件。 有关详细信息，请参阅[Visual Studio 命令表格 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

6. 测试、 调试和启动您的项目类型。

7. 显示的项目中**项目**选项卡**添加引用**对话框中，通过设置`VARIANT_TRUE`的值作为`VSHPROPID_ShowProjInSolutionPage`。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>。

8. 创建 Microsoft 安装程序 ( *.msi*) 安装你的 Vspackage 的文件。 有关详细信息，请参阅[使用 Windows Installer 安装 Vspackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)，[注册项目类型](../../extensibility/internals/registering-a-project-type.md)，并[Vspackage](../../extensibility/internals/vspackages.md)。

## <a name="see-also"></a>请参阅
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [何时创建项目类型](../../extensibility/internals/when-to-create-project-types.md)
- [创建项目类型](../../extensibility/internals/creating-project-types.md)