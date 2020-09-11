---
title: 自动化模型概述 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], about automation
- extensibility
ms.assetid: 12b6d6db-0d22-4aaa-aa7d-1365f759b7b0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7f953add14c617d54d44cf8d6bf873c28eea8651
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012160"
---
# <a name="automation-model-overview"></a>自动化模型概述
自动化模型包含一组对象，您可以对这些对象编写 Visual Studio 外接程序或扩展。 外接程序是一个可操作 Visual Studio 环境和自动化常见任务的应用程序。 Visual Studio 扩展可以创建自定义 Visual Studio 组件或添加到标准组件（如文本编辑器）的功能。

## <a name="objects-in-the-automation-model"></a>自动化模型中的对象
 自动化模型包含控制常见环境主要方面的对象的相关组。 下图显示了组成自动化模型的一组丰富的 Visual Studio 对象。

 ![Visual Studio 自动化对象图表](../../extensibility/internals/media/vsvisualstudioautomationobjectchart.gif "vsVisualStudioAutomationObjectChart")

 有关详细信息，请参阅 [扩展 Visual Studio 环境](/previous-versions/esk3eey8(v=vs.140))。

 环境为不同的功能区域提供了一个模型。 例如，你可能会在代码中找到各种元素的代码模型。 每个文档元素都有一个文档模型。 项目区域是一个区域，对 VSPackage 提供程序特别感兴趣。 你可能希望你的新项目类型以与自动化模型相同的方式向自动化模型提供 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 。 为 [Vspackage 提供自动化](../../extensibility/internals/providing-automation-for-vspackages.md)中概述了该过程。

 可以考虑扩展环境自动化模型的位置：

- Project

- 文档

- 代码

- 构建

有关自动化的详细信息，请参阅 [Visual Studio 的自动化和扩展性](../../vs-2015/extensibility/extensibility-in-visual-studio.md?view=vs-2015)。 本文档及其提供的文档可帮助你做出有关如何为你的 VSPackage 提供自动化的决策。

## <a name="see-also"></a>请参阅
- [如何：创建外接程序](/previous-versions/80493a3w(v=vs.140))