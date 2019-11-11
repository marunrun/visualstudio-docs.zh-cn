---
title: 自动化模型概述 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], about automation
- extensibility
ms.assetid: 12b6d6db-0d22-4aaa-aa7d-1365f759b7b0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6ea38dc79bd557f17bbae8276dd112304c9a40fa
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73186733"
---
# <a name="automation-model-overview"></a>自动化模型概述
自动化模型包含一组对象，您可以对这些对象编写 Visual Studio 外接程序或扩展。 外接程序是一个可操作 Visual Studio 环境和自动化常见任务的应用程序。 Visual Studio 扩展可以创建自定义 Visual Studio 组件或添加到标准组件（如文本编辑器）的功能。

## <a name="objects-in-the-automation-model"></a>自动化模型中的对象
 自动化模型包含控制常见环境主要方面的对象的相关组。 下图显示了组成自动化模型的一组丰富的 Visual Studio 对象。

 ![Visual Studio 自动化对象图表](../../extensibility/internals/media/vsvisualstudioautomationobjectchart.gif "vsVisualStudioAutomationObjectChart")

 有关详细信息，请参阅[扩展 Visual Studio 环境](https://msdn.microsoft.com/Library/4173a963-7ac7-4966-9bb7-e28a9d9f6792)。

 环境为不同的功能区域提供了一个模型。 例如，你可能会在代码中找到各种元素的代码模型。 每个文档元素都有一个文档模型。 项目区域是一个区域，对 VSPackage 提供程序特别感兴趣。 你可能希望你的新项目类型以与 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 和 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 参与自动化模型相同的方式向自动化模型提供。 为[Vspackage 提供自动化](../../extensibility/internals/providing-automation-for-vspackages.md)中概述了该过程。

 可以考虑扩展环境自动化模型的位置：

- 项目

- Document

- 代码

- 生成

有关自动化的详细信息，请参阅[Visual Studio 的自动化和扩展性](/visualstudio/extensibility/extensibility-in-visual-studio?view=vs-2015)。 本文档及其提供的文档可帮助你做出有关如何为你的 VSPackage 提供自动化的决策。

## <a name="see-also"></a>请参阅
- [如何：创建外接程序](https://msdn.microsoft.com/Library/50be56d2-e3a5-4cd2-8569-2a0666b268ce)