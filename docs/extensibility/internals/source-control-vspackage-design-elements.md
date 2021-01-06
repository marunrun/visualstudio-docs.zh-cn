---
title: 源代码管理 VSPackage 设计元素 |Microsoft Docs
description: 了解源代码管理 VSPackage 必须实现的结构，以及源代码管理 VSPackage 可以实现的接口和服务。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: e586470208989dce070c92963fc215f1053559a4
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877645"
---
# <a name="source-control-vspackage-design-elements"></a>源代码管理 VSPackage 设计元素
本节中的主题概述了源代码管理 VSPackage 为深度集成而必须实现的结构。 它还列出了源代码管理 VSPackage 可以实现的接口和服务，以及源代码管理 VSPackage 可以从其他组件中使用的接口和服务， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 以支持其源代码管理模型和功能。

## <a name="in-this-section"></a>本节内容
- [VSPackage 结构](../../extensibility/internals/vspackage-structure-source-control-vspackage.md)

 定义源代码管理 VSPackage 的结构。

- [相关服务和接口](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)

 列出源代码管理包相关的接口和服务。

- [提供的服务](../../extensibility/internals/services-provided-source-control-vspackage.md)

 介绍源代码管理 VSPackage 提供的源代码管理服务。

## <a name="related-sections"></a>相关章节
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)

 讨论如何创建一个源代码管理 VSPackage，该控件不仅提供源代码管理功能，还可用于自定义 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 源代码管理 UI。
