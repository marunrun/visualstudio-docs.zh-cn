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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8dfaf19e358d96b7737b06880d6fa4581b5c54f8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659373"
---
# <a name="validate-your-uml-model"></a>验证 UML 模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可在 Visual Studio 中绘制的某些 UML 模型在你的项目中可能被视作无效。 例如，你可能要求用例必须始终链接到序列图，序列图中具有表示用例的参与者的生命线。 您可以安装或定义帮助您的团队符合此类要求的*约束*。 约束可以在用户保存或打开模型时应用，可以由菜单命令调用。

 任何约束均不附带 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，因为它们依赖于团队解释和使用 UML 模型的方式。 但你可以定义你自己的约束，并安装由其他用户定义的约束。 若要了解如何定义约束并将其打包以进行分发，请参阅为[UML 模型定义验证约束](../modeling/define-validation-constraints-for-uml-models.md)。

## <a name="invoking-validation"></a>调用验证
 安装验证扩展后，可以在以下情况下应用它提供的约束。 某些约束设置为仅在某些情况下应用。

- **验证命令。** 若要随时调用验证，请单击 "**体系结构**" 菜单上的 "**验证 UML 模型**"。

  > [!NOTE]
  > 仅当安装了验证约束时，才显示该命令。

- **保存模型时。** 可以在保存模型时应用验证约束。 这些约束的目的在于帮助确保不保存你的项目解释为无效的模型。

   如有错误，系统将询问是否仍要保存该模型。 可以选择是要更正错误，还是仍然保存该模型。

- **打开模型时。** 打开某一模型时，可将验证方法应用于还原保存模型时存在的错误消息。 也可通过正在使用模型的不同部分的用户所做的更改之间的不一致引入错误。 有关详细信息，请参阅[共享模型和导出关系图](../modeling/share-models-and-exporting-diagrams.md)。

  在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 错误窗口中报告验证错误。

  若要在关系图中选择不正确的元素，请双击该错误。 这仅适用于在打开的关系图中可见的错误元素。

## <a name="installing-validation-constraints"></a>安装验证约束
 约束打包在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展 (VSIX) 文件内。 通常情况下，一组约束将是扩展的一部分，它也包含其他定义（如菜单命令、配置文件和工具箱项）。

#### <a name="to-install-a-visual-studio-extension"></a>安装 Visual Studio 扩展

1. 双击 Windows 资源管理器（或文件资源管理器）中的 **.vsix**文件。

2. 重新启动任何已在运行的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 实例。

## <a name="disabling-and-uninstalling-validation-constraints"></a>禁用和卸载验证约束
 需使用约束不适用的某一模型时，可以暂时禁用包含约束的扩展。 采用这种方式，便可以通过启用和禁用不同的扩展在不同的时间使用不同种类的模型。

#### <a name="to-disable-or-uninstall-a-visual-studio-extension"></a>禁用或卸载 Visual Studio 扩展

1. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]**工具**"菜单上，单击"**扩展和更新**"。

2. 在扩展旁，单击 "**禁用**" 以暂时禁用该扩展。 稍后可以通过返回到 "**扩展和更新**" 窗口重新启用它。

     \- 或 -

     单击 "**卸载**" 以删除扩展。

3. 重新启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。

## <a name="see-also"></a>请参阅
 [为 UML 模型定义验证约束为](../modeling/define-validation-constraints-for-uml-models.md)[应用创建模型](../modeling/create-models-for-your-app.md)[在开发过程中使用模型](../modeling/use-models-in-your-development-process.md)
