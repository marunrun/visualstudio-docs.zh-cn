---
title: 开发旧版语言服务 |Microsoft Docs
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
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6aa21b2f2e8b0321e829fd27fde1d833a63e7ecb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351578"
---
# <a name="develop-a-legacy-language-service"></a>开发旧版语言服务
此部分链接到主题可帮助您创建旧版语言服务。

 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要了解有关实现语言服务的新方法的详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。

## <a name="in-this-section"></a>本节内容
- [旧版语言服务模型](../../extensibility/internals/model-of-a-legacy-language-service.md)

 提供的最小语言服务模型[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]核心编辑器。 用于创建你自己的语言服务，可以作为指南使用此模型。

- [旧版语言服务接口](../../extensibility/internals/legacy-language-service-interfaces.md)

 讨论实现语言服务所需的对象，并提供了可用于提供语法突出显示、 方法数据和其他功能的其他对象的列表。

- [截获旧版语言服务命令](../../extensibility/internals/intercepting-legacy-language-service-commands.md)

 介绍如何将命令筛选器插入到你的语言服务为截距命令用来处理文本视图。

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service2.md)

 提供有关如何使用注册你的语言服务信息[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

- [用于调试的语言服务支持](../../extensibility/internals/language-service-support-for-debugging.md)

 介绍如何语言服务能够提供功能，可支持调试程序。

- [清单：创建旧版语言服务](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)

 提供用于创建和集成核心编辑器的语言服务的分步说明。

## <a name="related-sections"></a>相关章节
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 讨论如何实现语法突出显示语言服务中。

- [旧版语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)

 介绍了语句完成时，所依据的语言服务可帮助用户完成语言关键字或在开始键入的元素的过程。

- [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)

 介绍如何为重载的函数和方法提供方法的提示。

- [如何：提供旧版语言服务中的隐藏的文本支持](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)

 介绍隐藏的文本区域的目的，并提供有关如何实现隐藏的文本区域的说明。

- [如何：提供旧版语言服务中的展开大纲显示支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)

 介绍扩展对你超出支持的语言的大纲显示支持的两个选项*折叠到定义*命令。