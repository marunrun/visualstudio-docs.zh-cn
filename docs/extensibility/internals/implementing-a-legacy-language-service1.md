---
title: 实现传统语言服务1 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, managed
ms.assetid: df638f24-166d-4b80-be82-c9c39ca7a556
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c3805e49ffa83f7dea2ee58ef36e1bc8e48b1eaa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707688"
---
# <a name="implementing-a-legacy-language-service"></a>实现旧版语言服务
您可以使用托管包框架 （MPF） 中的类来实现支持各种功能的传统语言服务，例如语法突出显示、大括号匹配和 IntelliSense 完成。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解有关实现语言服务的新方法的详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="in-this-section"></a>本节内容
- [旧版语言服务概述](../../extensibility/internals/legacy-language-service-overview.md)

 MPF 中支持的语言服务功能概述。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 描述使用 MPF 实现语言服务所需的内容。

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)

 描述向[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]注册基于 MPF 的语言服务所需的步骤。

- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 描述使用 MPF 实现语言服务的所有功能所需的两个解析器。

- [演练：创建旧版语言服务](../../extensibility/internals/walkthrough-creating-a-legacy-language-service.md)

 提供在 VS 包中实现 MPF 语言服务所需的基本步骤。

- [演练：获取安装代码片段（旧版实现）的列表](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)

 演示检索已安装代码段列表的技术。

- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)

 提供指向主题的链接，详细说明使用 MPF 实现语言服务的所有功能必须做什么。
