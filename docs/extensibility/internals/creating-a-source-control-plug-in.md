---
title: 创建源代码管理插件 |Microsoft Docs
description: 了解如何创建将源代码管理功能添加到 Visual Studio 集成开发环境 (IDE) 的源代码管理插件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- plug-ins, source control
- source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: c7e69fa4-150e-469a-a6fc-fa1260bdbb07
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5ae887e8752e1603af173ed569d19a6602ac84f0
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305381"
---
# <a name="create-a-source-control-plug-in"></a>创建源代码管理插件
Visual Studio SDK 提供了一些资源，可用于将源代码管理功能添加到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (IDE) 的集成开发环境。 它允许你使用任何符合本文档中所述源代码管理插件 API 的插件 DLL。

## <a name="in-this-section"></a>在本节中
- [入门](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)

 描述如何安装源代码管理插件并突出显示当前可用的源代码管理插件 API 版本。

- [体系结构](../../extensibility/internals/source-control-plug-in-architecture.md)

 使用体系结构关系图说明源代码管理插件与 IDE 的集成 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)

 提供有关如何测试源代码管理插件的安装和操作的指导。

## <a name="related-sections"></a>相关章节
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)

 讨论如何创建一个源代码管理 VSPackage，该控件不仅提供源代码管理功能，而且还替换 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 源代码管理 UI。

- [源代码管理插件](../../extensibility/source-control-plug-ins.md)

 提供源代码管理插件 API 中所有元素的完整列表。

- [源代码管理](../../extensibility/internals/source-control.md)

 讨论用于实现作为的集成功能的源代码管理的选项 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。
