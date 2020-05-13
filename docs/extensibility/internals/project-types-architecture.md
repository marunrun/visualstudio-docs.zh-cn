---
title: 项目类型体系结构 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], architecture
ms.assetid: 9c1d940f-8a54-41f7-a8aa-c870e324371c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e53929b1ec2ed9c73191bf16f1cedc84a53b58f2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706311"
---
# <a name="project-types-architecture"></a>项目类型体系结构
本节包含有关 中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目类型的体系结构的详细信息。

## <a name="in-this-section"></a>本节内容
- [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)

 列出项目类型可以使用的服务及其必须实现的接口。

- [项目模型核心组件](../../extensibility/internals/project-model-core-components.md)

 描述项目类型必须实现，可选地可以实现，以提供其他功能。

- [何时创建项目类型](../../extensibility/internals/when-to-create-project-types.md)

 帮助您确定何时必须创建项目类型，以及何时可以使用另一个[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]扩展性功能（如 VSPackages 和编辑器）来实现相同的目标。

- [层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)

 描述如何使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]层次结构和选择上下文来提供一致和简化的用户体验。

## <a name="related-sections"></a>相关章节
- [项目子类型](../../extensibility/internals/project-subtypes.md)

 说明项目子类型如何自定义[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]和[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]的项目系统的行为。

- [项目类型](../../extensibility/internals/project-types.md)

 提供项目概述，作为[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE） 的基本构建基块。 链接指向其他主题，这些主题解释了项目如何控制构建和编译代码。
