---
title: 传统语言服务功能2 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], code development aides
ms.assetid: 97c38622-ae0b-4ae0-90ed-604072c298d3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 33f12e816476aa54f334988b99b9e86e820784f6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707375"
---
# <a name="legacy-language-service-features"></a>旧版语言服务功能
以下主题列出了您可以提供的一些旧语言服务功能。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解有关实现语言服务的新方法的详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="in-this-section"></a>本节内容
- [在旧版语言服务中进行语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 说明如何实现语法着色。

- [在旧版语言服务中进行自动格式设置](../../extensibility/internals/automatic-formatting-in-a-legacy-language-service.md)

 说明如何实现自动格式化。

- [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)

 说明如何实现 IntelliSense 参数信息工具提示。

- [旧版语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)

 说明如何实现 IntelliSense 语句列表和成员完成列表。

- [旧版语言服务中的大纲显示和隐藏文本](../../extensibility/internals/outlining-and-hidden-text-in-a-legacy-language-service.md)

 说明如何实现大纲或隐藏文本。

- [如何：提供旧版语言服务中扩展的大纲显示支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)

 解释实现调试器支持的一些步骤。

## <a name="related-sections"></a>相关章节
