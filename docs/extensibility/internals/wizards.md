---
title: 向导 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], providing wizard support
ms.assetid: 59d9a77f-ee80-474b-a14f-90f477ab717b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e3b17d7ef3137c48ddda97e1b2b5bbf0e58cf5bb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312839"
---
# <a name="wizards"></a>向导
创建向导后，你通常想要将其添加到[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 (IDE)，以便其他人可以使用它。 添加了的向导随后会出现**添加新项目**或**添加新项**对话框。 若要查看**添加新项目**或**添加新项**对话框框中，右键单击打开的解决方案中**解决方案资源管理器**，指向**添加**，和然后单击**新的项目**或**新项**。

 向导可以在中实现[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]让用户在打开时的可用值在树视图中选择**添加新项目**对话框或**添加新项**对话框中，或当他们右键单击中的项**解决方案资源管理器**。

 在向导中，您可以提供本地化的新项目或 ite，名称的选项，可以确定当用户选择该向导时，用户将看到的图标。 此外可以控制相对于其他可用的项目; 出现新项的顺序项不需要按字母顺序组织。

 此外可以提供一个向导，以不同的方式，启动基于传递给该向导打开时的自定义参数。

 在本部分中的主题讨论用于实现导致的文件[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**添加新项目**并**添加新项**若要列出可用的向导和模板，在向导的对话框和您的向导在 IDE 中正常运行而必须满足的要求。

## <a name="in-this-section"></a>本节内容
- [模板目录说明 (.Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)

 概述了哪个模板的目录说明文件并说明如何显示文件夹、 向导.vsz 文件和与访问的对话框中的项目相关联的模板文件在 IDE 中的工作方式。

- [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)

 介绍如何在 IDE 启动向导，并列出.vsz 文件的三个部分。

- [向导界面 (IDTWizard)](../../extensibility/internals/wizard-interface-idtwizard.md)

 介绍`IDTWizard`向导为在 IDE 中工作而必须实现的接口。

- [上下文参数](../../extensibility/internals/context-parameters.md)

 介绍如何实现向导和 IDE 将上下文参数传递给实现时会发生什么情况。

- [自定义参数](../../extensibility/internals/custom-parameters.md)

 介绍如何使用自定义参数启动该向导后控制向导的操作。

## <a name="related-sections"></a>相关章节
- [项目类型](../../extensibility/internals/project-types.md)

 提供指向其他主题提供有关如何设计新的项目类型的信息。

- [扩展项目](../../extensibility/extending-projects.md)

 介绍如何使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目和解决方案来组织代码文件和资源文件，以及如何实现源代码管理。