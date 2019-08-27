---
title: 实现旧版语言服务 1 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, managed
ms.assetid: df638f24-166d-4b80-be82-c9c39ca7a556
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 626838b0e82846f66b817465fca2df353af42dd5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66315649"
---
# <a name="implementing-a-legacy-language-service"></a>实现旧版语言服务
您可以使用托管的包框架 (MPF) 中的类来实现旧版语言服务支持各种功能，如语法突出显示、 大括号匹配和 IntelliSense 完成。

 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要了解有关实现语言服务的新方法的详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。

## <a name="in-this-section"></a>本节内容
- [旧版语言服务概述](../../extensibility/internals/legacy-language-service-overview.md)

 MPF 中支持的语言服务功能的概述。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 介绍什么是通过使用 MPF 实现语言服务所必需。

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)

 介绍的步骤所需注册一种基于 MPF 的语言服务，具有[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 介绍通过使用 MPF 实现的语言服务的所有功能所需的两个分析器。

- [演练：创建旧版语言服务](../../extensibility/internals/walkthrough-creating-a-legacy-language-service.md)

 提供在 VSPackage 中实现的 MPF 语言服务所需的基本步骤。

- [演练：获取包含已安装的代码片段的列表（旧版实现）](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)

 演示如何检索已安装的代码片段的列表的技术。

- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)

 提供主题的链接必须做什么来使用 MPF 实现的语言服务的所有功能的详细信息。