---
title: 验证 UML 模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML, constraints
- UML, validation
ms.assetid: deed5092-c11d-4431-a801-1e866a103075
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f795928677f4a232c3ae3cec0d3bab9d9266cb35
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63437458"
---
# <a name="validate-your-uml-model"></a>验证 UML 模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可在 Visual Studio 中绘制的某些 UML 模型在你的项目中可能被视作无效。 例如，你可能要求用例必须始终链接到序列图，序列图中具有表示用例的参与者的生命线。 可以安装或定义*约束*帮助团队符合这样的要求。 约束可以在用户保存或打开模型时应用，可以由菜单命令调用。  
  
 任何约束均不附带 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，因为它们依赖于团队解释和使用 UML 模型的方式。 但你可以定义你自己的约束，并安装由其他用户定义的约束。 若要了解如何定义约束并将其打包进行分发，请参阅[为 UML 模型定义验证约束](../modeling/define-validation-constraints-for-uml-models.md)。  
  
## <a name="invoking-validation"></a>调用验证  
 安装验证扩展后，可以在以下情况下应用它提供的约束。 某些约束设置为仅在某些情况下应用。  
  
- **验证命令。** 若要调用在任何时间验证，请单击**验证 UML 模型**上**体系结构**菜单。  
  
  > [!NOTE]
  > 仅当安装了验证约束时，才显示该命令。  
  
- **在保存模型时。** 可以在保存模型时应用验证约束。 这些约束的目的在于帮助确保不保存你的项目解释为无效的模型。  
  
   如有错误，系统将询问是否仍要保存该模型。 可以选择是要更正错误，还是仍然保存该模型。  
  
- **在打开某一模型。** 打开某一模型时，可将验证方法应用于还原保存模型时存在的错误消息。 也可通过正在使用模型的不同部分的用户所做的更改之间的不一致引入错误。 有关详细信息，请参阅[共享模型和导出关系图](../modeling/share-models-and-exporting-diagrams.md)。  
  
  在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 错误窗口中报告验证错误。  
  
  若要在关系图中选择不正确的元素，请双击该错误。 这仅适用于在打开的关系图中可见的错误元素。  
  
## <a name="installing-validation-constraints"></a>安装验证约束  
 约束打包在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展 (VSIX) 文件内。 通常情况下，一组约束将是扩展的一部分，它也包含其他定义（如菜单命令、配置文件和工具箱项）。  
  
#### <a name="to-install-a-visual-studio-extension"></a>安装 Visual Studio 扩展  
  
1. 双击 **.vsix**在 Windows 资源管理器 （或文件资源管理器） 中的文件。  
  
2. 重新启动任何已在运行的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 实例。  
  
## <a name="disabling-and-uninstalling-validation-constraints"></a>禁用和卸载验证约束  
 需使用约束不适用的某一模型时，可以暂时禁用包含约束的扩展。 采用这种方式，便可以通过启用和禁用不同的扩展在不同的时间使用不同种类的模型。  
  
#### <a name="to-disable-or-uninstall-a-visual-studio-extension"></a>禁用或卸载 Visual Studio 扩展  
  
1. 上[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]**工具**菜单中，单击**扩展和更新**。  
  
2. 扩展的旁边，单击**禁用**暂时禁用该扩展。 您可以重新启用它更高版本返回给**扩展和更新**窗口。  
  
     \- 或 -  
  
     单击**卸载**以删除该扩展。  
  
3. 重新启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [为 UML 模型定义验证约束](../modeling/define-validation-constraints-for-uml-models.md)   
 [为您的应用程序创建模型](../modeling/create-models-for-your-app.md)   
 [在你的开发过程中使用模型](../modeling/use-models-in-your-development-process.md)
