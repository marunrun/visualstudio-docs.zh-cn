---
title: 清单：创建新的项目类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating new types
- project types, checklist for creating
ms.assetid: 29eb9c3b-1933-4741-aa85-65a33f0825ba
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 02edc5925109a31eebfd98c90bd116fb86eef276
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697231"
---
# <a name="checklist-creating-new-project-types"></a>清单：创建新的项目类型
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

若要创建新的项目类型，必须完成多个任务。 以下清单提供了这些任务的指南。  
  
1. 设计新项目类型的功能。 有关详细信息，请参阅 [项目类型设计决策](../../extensibility/internals/project-type-design-decisions.md)。  
  
2. 确定哪些编辑器用于代码和其他项目元素。 您可以使用核心或标准编辑器，也可以创建和使用特定于项目的编辑器。 有关详细信息，请参阅 [创建自定义编辑器和设计器](../../extensibility/creating-custom-editors-and-designers.md) 和 [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)。  
  
3. 确定项目项在 **类视图** 和 **对象浏览器**中的参与程度。 有关详细信息，请参阅 [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)。  
  
4. 基于你之前为项目和项目项所做的设计决策派生新类。  
  
5. 为以下项目类型组件编写代码：  
  
    - 项目工厂，用于管理创建新项目和打开现有项目。 有关详细信息，请参阅 [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)。  
  
    - 项目层次结构和命令处理。 有关详细信息，请参阅 [不在生成中：使用 HierUtil7 项目类实现项目类型 (c + +) ](https://msdn.microsoft.com/a5c16a09-94a2-46ef-87b5-35b815e2f346)、 [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)、 [项目模型核心组件](../../extensibility/internals/project-model-core-components.md) 和 [menucommand 与 OleMenuCommands](../../misc/menucommands-vs-olemenucommands.md)。  
  
    - 项目项管理，包括将项目添加到 " **新建项目** " 对话框。 有关详细信息，请参阅 [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md) 和 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)。  
  
    - 项目状态和各个项的持久性。 有关详细信息，请参阅 [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)。 有关解决方案信息的持久性，请参阅 [解决方案](../../extensibility/internals/solutions-overview.md)。  
  
    - 要在属性窗口中显示的配置独立属性。 有关详细信息，请参阅 [扩展属性](../../extensibility/internals/extending-properties.md)。  
  
    - 在属性页中实现的项目配置属性，用于显示与配置相关的属性。 有关详细信息，请参阅 [管理配置选项](../../extensibility/internals/managing-configuration-options.md)。  
  
    - 枚举部署的输出。 有关详细信息，请参阅 [输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)。  
  
    - 项目启动服务。 有关详细信息，请参阅 [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md) 和 [项目模型核心组件](../../extensibility/internals/project-model-core-components.md)。  
  
    - 对象或从派生的类 `IDispatch` 可用于实现自动化。  
  
    - XML 命令表 ( .vsct) 文件。 有关详细信息，请参阅 [Visual Studio Command Table (.Vsct) Files](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。  
  
6. 测试、调试和启动项目类型。  
  
7. 通过将设置为的值，在 "**添加引用**" 对话框的 "**项目**" 选项卡中显示你的项目 `VARIANT_TRUE` `VSHPROPID_ShowProjInSolutionPage` 。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>。  
  
8. 创建 Microsoft Installer ( .msi) 文件以安装 Vspackage。 有关详细信息，请参阅 [使用 Windows Installer 安装 vspackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)、 [注册项目类型](../../extensibility/internals/registering-a-project-type.md)和 [vspackage](../../extensibility/internals/vspackages.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)   
 [何时创建项目类型](../../extensibility/internals/when-to-create-project-types.md)   
 [创建项目类型](../../extensibility/internals/creating-project-types.md)
