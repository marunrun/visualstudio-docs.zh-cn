---
title: 创建源代码管理插件 |微软文档
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
ms.openlocfilehash: 9e0d9dc54a61cabe7bdd5c21c10abf0def34ff6a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709170"
---
# <a name="create-a-source-control-plug-in"></a>创建源代码管理插件
Visual Studio SDK 提供的资源使您能够向[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE） 添加源代码管理功能。 它允许您使用任何符合本文档中概述的源代码管理插件 API 的插件 DLL。

## <a name="in-this-section"></a>在本节中
- [入门](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)

 描述如何安装源代码管理插件并突出显示当前可用的源代码管理插件 API 版本。

- [体系结构](../../extensibility/internals/source-control-plug-in-architecture.md)

 使用体系结构图来解释源代码管理插件与 IDE 的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成。

- [测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)

 提供有关如何测试源代码管理插件的安装和操作的指导。

## <a name="related-sections"></a>相关章节
- [创建源代码管理 VS 包](../../extensibility/internals/creating-a-source-control-vspackage.md)

 讨论如何创建源代码管理 VSPackage，该源代码管理不仅提供源代码管理功能，而且替换[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]源代码管理 UI。

- [源代码管理插件](../../extensibility/source-control-plug-ins.md)

 提供源代码管理插件 API 中所有元素的完整列表。

- [源代码管理](../../extensibility/internals/source-control.md)

 讨论了实现源代码管理作为 的集成功能的选项[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。
