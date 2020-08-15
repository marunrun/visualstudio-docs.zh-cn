---
title: 旧版语言服务 Features2 |Microsoft Docs
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
ms.openlocfilehash: 04e7df7fc5c7532d2db45bc2b643a249d1e566c7
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88237901"
---
# <a name="legacy-language-service-features-2"></a>旧版语言服务功能2
以下主题列出了你可以提供的一些旧版语言服务功能。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解有关实现语言服务的新方法的详细信息，请参阅 [编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="in-this-section"></a>本节内容
- [在旧版语言服务中进行语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 说明如何实现语法着色。

- [在旧版语言服务中进行自动格式设置](../../extensibility/internals/automatic-formatting-in-a-legacy-language-service.md)

 说明如何实现自动格式设置。

- [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)

 说明如何实现 IntelliSense 参数信息工具提示。

- [旧版语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)

 说明如何实现 IntelliSense 语句列表和成员完成列表。

- [旧版语言服务中的大纲显示和隐藏文本](../../extensibility/internals/outlining-and-hidden-text-in-a-legacy-language-service.md)

 说明如何实现大纲显示或隐藏文本。

- [如何：提供旧版语言服务中扩展的大纲显示支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)

 介绍实现调试器支持的一些步骤。

## <a name="related-sections"></a>相关章节
