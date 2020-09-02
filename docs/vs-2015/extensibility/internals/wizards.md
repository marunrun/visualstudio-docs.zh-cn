---
title: 向导 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], providing wizard support
ms.assetid: 59d9a77f-ee80-474b-a14f-90f477ab717b
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6e58ebd736f7bb9f35df6e41d5235f36f7037259
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687620"
---
# <a name="wizards"></a>向导
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建向导后，通常需要将其添加到 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 集成开发环境中 (IDE) ，以便其他人可以使用它。 添加的向导随后会出现在 " **添加新项目** " 或 " **添加新项** " 对话框中。 若要查看 " **添加新项目** " 或 " **添加新项** " 对话框，请在 **解决方案资源管理器**中右键单击打开的解决方案，指向 " **添加**"，然后单击 " **新建项目** " 或 " **新建项**"。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]当用户打开 "**添加新项目**" 对话框或 "**添加新项**" 对话框，或在**解决方案资源管理器**中右键单击某项时，可以在中实现，以允许用户从可用值的树视图中进行选择。  
  
 在向导中，您可以提供对新项目或 ites 的名称进行本地化的选项，并且可以确定用户在选择该向导时将看到的图标。 您还可以控制新项相对于其他可用项的显示顺序;不需要按字母顺序对项进行组织。  
  
 你还可以根据在打开时传递到向导的自定义参数，提供以不同方式启动的向导。  
  
 本节中的主题讨论您实现的用于使 " [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **添加新项目** " 和 " **添加新项** " 对话框在可用向导和模板之间列出向导的文件，以及您的向导在 IDE 中正确运行时必须满足的要求。  
  
## <a name="in-this-section"></a>本节内容  
 [模板目录说明 (.Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)  
 概述了模板目录说明文件的内容，并说明了这些文件在 IDE 中如何在 IDE 中显示文件夹、向导 .vsz 文件以及与对话框中的项目相关联的模板文件。  
  
 [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)  
 说明 IDE 如何启动向导，并列出 .vsz 文件的三个部分。  
  
 [向导界面 (IDTWizard)](../../extensibility/internals/wizard-interface-idtwizard.md)  
 介绍 `IDTWizard` 向导在 IDE 中工作时必须实现的接口。  
  
 [上下文参数](../../extensibility/internals/context-parameters.md)  
 说明如何实现向导以及 IDE 将上下文参数传递到实现时所发生的情况。  
  
 [自定义参数](../../extensibility/internals/custom-parameters.md)  
 说明如何在向导启动后使用自定义参数控制向导的操作。  
  
## <a name="related-sections"></a>相关章节  
 [项目类型](../../extensibility/internals/project-types.md)  
 提供指向其他主题的链接，这些主题提供有关如何设计新的项目类型的信息。  
  
 [演练：创建向导](https://msdn.microsoft.com/library/adb41fe9-fcca-4e87-bf4f-bf2fa68e8b06)  
 阐释如何创建向导。  
  
 [扩展项目](../../extensibility/extending-projects.md)  
 介绍如何使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 项目和解决方案来组织代码文件和资源文件，以及如何实现源代码管理。
