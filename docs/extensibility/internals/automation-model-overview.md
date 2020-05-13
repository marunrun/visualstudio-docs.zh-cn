---
title: 自动化模型概述 |微软文档
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
ms.openlocfilehash: 7b940677c370106ebdcc63c7984d553003251e8a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710007"
---
# <a name="automation-model-overview"></a>自动化模型概述
自动化模型由一组对象组成，您可以编写 Visual Studio 外接程序或扩展。 外接程序是一个可以操作 Visual Studio 环境并自动执行常见任务的应用程序。 Visual Studio 扩展可以创建自定义 Visual Studio 组件或添加到标准组件（如文本编辑器）的功能。

## <a name="objects-in-the-automation-model"></a>自动化模型中的对象
 自动化模型由控制公共环境主要方面的相关对象组组成。 下图显示了组成自动化模型的大量 Visual Studio 对象。

 ![可视化工作室自动化对象图](../../extensibility/internals/media/vsvisualstudioautomationobjectchart.gif "vsVisualStudio自动化对象图表")

 有关详细信息，请参阅[扩展可视化工作室环境](https://msdn.microsoft.com/Library/4173a963-7ac7-4966-9bb7-e28a9d9f6792)。

 环境为不同的功能区域提供了一个模型。 例如，在代码中可以找到各种元素的代码模型。 有各种文档元素的文档模型。 一个领域，即项目区域，对 VSPackage 提供商特别感兴趣。 您可能希望新的项目类型以与自动化模型相同的方式[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]对自动化模型[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]做出贡献。 该过程在[提供 VSPackages 的自动化](../../extensibility/internals/providing-automation-for-vspackages.md)中进行了概述。

 可以考虑扩展环境自动化模型的位置：

- Project

- Document

- 代码

- 生成

有关自动化的详细信息，请参阅[可视化工作室的自动化和可扩展性](/visualstudio/extensibility/extensibility-in-visual-studio?view=vs-2015)。 本文档及其提供的链接可帮助您做出有关如何为 VSPackage 提供自动化的决策。

## <a name="see-also"></a>请参阅
- [如何：创建外接程序](https://msdn.microsoft.com/Library/50be56d2-e3a5-4cd2-8569-2a0666b268ce)
