---
title: 向导 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], providing wizard support
ms.assetid: 59d9a77f-ee80-474b-a14f-90f477ab717b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d65cf2dcc10380b0ac750c8e1b0e7fd56eab95b5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703213"
---
# <a name="wizards"></a>向导
创建向导后，通常需要将其添加到[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE），以便其他人可以使用它。 然后，添加的向导将显示在"**添加新项目**"或 **"添加新项目"** 对话框中。 要查看"**添加新项目**"或 **"添加新项目"** 对话框，请右键单击**解决方案资源管理器**中的打开解决方案，指向 **"添加**"，然后单击"**新项目**"或 **"新项目**"。

 向导可以实现，以便用户[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]在打开 **"添加新项目**"对话框或 **"添加新项目**"对话框时，或在**解决方案资源管理器**中右键单击项目时，从可用值的树视图中选择。

 在向导中，可以提供本地化新项目或 ites 名称的选项，还可以确定用户在选择向导时将看到的图标。 您还可以控制新项目相对于其他可用项的显示顺序;项目不必按字母顺序排列。

 还可以提供不同启动的向导，该向导基于打开向导时传递给向导的自定义参数。

 本节中的主题讨论您实现的文件，以便导致[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**"添加新项目和****添加新项目"** 对话框，以在可用的向导和模板中列出向导，以及向导必须满足的要求才能在 IDE 中正常运行。

## <a name="in-this-section"></a>本节内容
- [模板目录说明 (.Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)

 提供哪些模板目录描述文件的概述，并解释它们如何在 IDE 中工作以显示对话框中与项目关联的文件夹、向导 .vsz 文件和模板文件。

- [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)

 解释 IDE 如何启动向导并列出 .vsz 文件的三个部分。

- [向导界面 (IDTWizard)](../../extensibility/internals/wizard-interface-idtwizard.md)

 描述向导`IDTWizard`在 IDE 中工作时必须实现的接口。

- [上下文参数](../../extensibility/internals/context-parameters.md)

 说明如何实现向导，以及当 IDE 将上下文参数传递给实现时会发生什么。

- [自定义参数](../../extensibility/internals/custom-parameters.md)

 说明在向导启动后如何使用自定义参数来控制向导的操作。

## <a name="related-sections"></a>相关章节
- [项目类型](../../extensibility/internals/project-types.md)

 提供指向其他主题的链接，这些主题提供有关如何设计新项目类型的信息。

- [扩展项目](../../extensibility/extending-projects.md)

 介绍如何使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目和解决方案来组织代码文件和资源文件，以及如何实现源代码管理。
