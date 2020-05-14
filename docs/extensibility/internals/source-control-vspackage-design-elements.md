---
title: 源代码管理 VS 包设计元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, design elements
ms.assetid: edd3f2ff-ca32-4465-8ace-4330493b67bb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b5e94829f781c058d9b0ea56cdec6c03c71ffe0c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705000"
---
# <a name="source-control-vspackage-design-elements"></a>源代码管理 VSPackage 设计元素
本节中的主题概述了源控件 VSPackage 实现深度集成时必须实现的结构。 它还列出了源代码管理 VSPackage 可以实现的接口和服务，以及源代码管理 VSPackage 可以从其他[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]组件使用的接口和服务来支持其源代码管理模型和功能。

## <a name="in-this-section"></a>本节内容
- [VSPackage 结构](../../extensibility/internals/vspackage-structure-source-control-vspackage.md)

 定义源代码管理 VSPackage 的结构。

- [相关服务和接口](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)

 列出与源代码管理包相关的接口和服务。

- [提供的服务](../../extensibility/internals/services-provided-source-control-vspackage.md)

 描述源代码管理 VSPackage 提供的源代码管理服务。

## <a name="related-sections"></a>相关章节
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)

 讨论如何创建源代码管理 VSPackage，该源代码管理不仅提供源代码管理功能，还可用于自定义[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]源代码管理 UI。
