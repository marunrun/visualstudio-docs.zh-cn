---
title: 旧版语言服务功能 2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], code development aides
ms.assetid: 97c38622-ae0b-4ae0-90ed-604072c298d3
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: de7e0fa6a229929a34ed3654c3a4e03e02d1129b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333503"
---
# <a name="legacy-language-service-features"></a>旧版语言服务功能
以下主题列出了一些可以提供的旧版语言服务功能。

 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要了解有关实现语言服务的新方法的详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。

## <a name="in-this-section"></a>本节内容
- [在旧版语言服务中进行语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 介绍如何实现语法着色。

- [在旧版语言服务中进行自动格式设置](../../extensibility/internals/automatic-formatting-in-a-legacy-language-service.md)

 介绍如何实现自动格式设置。

- [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)

 介绍如何实现 IntelliSense 参数信息工具提示。

- [旧版语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)

 介绍如何实现 IntelliSense 语句列表和成员完成列表。

- [旧版语言服务中的大纲显示和隐藏文本](../../extensibility/internals/outlining-and-hidden-text-in-a-legacy-language-service.md)

 介绍如何实现的大纲显示或隐藏的文本。

- [如何：提供旧版语言服务中扩展的大纲显示支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)

 介绍了某些实现调试器支持中的步骤...

## <a name="related-sections"></a>相关章节