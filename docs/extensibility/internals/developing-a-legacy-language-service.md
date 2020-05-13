---
title: 开发传统语言服务 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.vsip.LangServWiz.langtoks
- vs.vsip.LangServWiz.welcome
- vs.vsip.LangServWiz.langSpec
- vs.vsip.LangServWiz.langInfo
- vs.vsip.LangServWiz.langServOpts
helpviewer_keywords:
- language services, developing
ms.assetid: 6151ba88-c1c3-41de-a1cc-668f494d48d1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0c7f930d5087b6a822156fd44024def0d5b42b49
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708672"
---
# <a name="develop-a-legacy-language-service"></a>开发传统语言服务
本节链接到可帮助您创建旧语言服务的主题。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解有关实现语言服务的新方法的详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="in-this-section"></a>在本节中
- [传统语言服务的模型](../../extensibility/internals/model-of-a-legacy-language-service.md)

 为[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]核心编辑器提供最小语言服务的模型。 您可以使用此模型作为创建您自己的语言服务的指南。

- [旧语言服务接口](../../extensibility/internals/legacy-language-service-interfaces.md)

 讨论实现语言服务所需的对象，并提供可用于提供语法突出显示、方法数据和其他功能的其他对象的列表。

- [拦截旧语言服务命令](../../extensibility/internals/intercepting-legacy-language-service-commands.md)

 描述如何将命令筛选器插入到语言服务中，以拦截文本视图将处理的命令。

- [注册旧语言服务](../../extensibility/internals/registering-a-legacy-language-service2.md)

 提供有关如何使用 注册语言服务的信息[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

- [用于调试的语言服务支持](../../extensibility/internals/language-service-support-for-debugging.md)

 描述语言服务如何提供支持调试器的功能。

- [检查表：创建旧语言服务](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)

 提供用于为核心编辑器创建和集成语言服务的分步说明。

## <a name="related-sections"></a>相关章节
- [旧语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 讨论如何在语言服务中实现语法突出显示。

- [旧语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)

 讨论语句完成，语言服务帮助用户完成他们已经开始键入的语言关键字或元素的过程。

- [旧语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)

 描述如何为重载函数和方法提供方法提示。

- [如何：在旧语言服务中提供隐藏文本支持](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)

 解释隐藏文本区域的用途，并提供有关如何实现隐藏文本区域的说明。

- [如何：在传统语言服务中提供扩展的大纲支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)

 解释将概述对语言的支持扩展到支持"*折叠到定义"命令的*两个选项。
