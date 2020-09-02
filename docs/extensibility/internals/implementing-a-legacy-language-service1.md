---
title: 实现旧版语言 Service1 |Microsoft Docs
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
ms.openlocfilehash: 2535c527fc3d2d94609246959c5293e455b9808d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "88238733"
---
# <a name="implementing-a-legacy-language-service-1"></a>实现旧版语言服务1
可以在托管包框架中使用类 (MPF) 来实现支持各种功能（如语法突出显示、大括号匹配和 IntelliSense 完成）的旧版语言服务。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解有关实现语言服务的新方法的详细信息，请参阅 [编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="in-this-section"></a>本节内容
- [旧版语言服务概述](../../extensibility/internals/legacy-language-service-overview.md)

 MPF 支持的语言服务功能概述。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 介绍使用 MPF 实现语言服务所需的内容。

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)

 描述使用注册基于 MPF 的语言服务所需的步骤 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 描述使用 MPF 实现语言服务的所有功能所需的两个分析器。

- [演练：创建旧版语言服务](../../extensibility/internals/walkthrough-creating-a-legacy-language-service.md)

 提供在 VSPackage 中实现 MPF 语言服务所需的基本步骤。

- [演练：获取包含已安装的代码片段的列表（旧版实现）](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)

 演示检索已安装代码段列表的方法。

- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)

 提供相关主题的链接，这些主题详细说明了使用 MPF 实现语言服务的所有功能时必须执行的操作。
