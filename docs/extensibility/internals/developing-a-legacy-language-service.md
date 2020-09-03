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
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0c7f930d5087b6a822156fd44024def0d5b42b49
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708672"
---
# <a name="develop-a-legacy-language-service"></a>开发旧版语言服务
本部分链接到帮助你创建旧版语言服务的主题。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解有关实现语言服务的新方法的详细信息，请参阅 [编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="in-this-section"></a>本节内容
- [旧版语言服务的模型](../../extensibility/internals/model-of-a-legacy-language-service.md)

 为核心编辑器提供最小语言服务的模型 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 您可以使用此模型作为创建自己的语言服务的指南。

- [旧版语言服务接口](../../extensibility/internals/legacy-language-service-interfaces.md)

 讨论实现语言服务所需的对象，并提供可用于提供语法突出显示、方法数据和其他功能的其他对象的列表。

- [截获旧版语言服务命令](../../extensibility/internals/intercepting-legacy-language-service-commands.md)

 介绍如何在语言服务中插入命令筛选器，以截获文本视图要处理的命令。

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service2.md)

 提供有关如何使用注册语言服务的信息 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [用于调试的语言服务支持](../../extensibility/internals/language-service-support-for-debugging.md)

 描述语言服务如何提供支持调试器的功能。

- [清单：创建旧版语言服务](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)

 提供为核心编辑器创建和集成语言服务的分步说明。

## <a name="related-sections"></a>相关章节
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 讨论如何在语言服务中实现语法突出显示。

- [旧版语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)

 讨论语句完成，即语言服务帮助用户完成其已开始键入的 language 关键字或元素的过程。

- [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)

 介绍如何提供重载函数和方法的方法提示。

- [如何：在旧版语言服务中提供隐藏的文本支持](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)

 说明隐藏文本区域的用途，并提供有关如何实现隐藏文本区域的说明。

- [如何：提供旧版语言服务中的扩展大纲支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)

 介绍用于扩展对语言的大纲支持的两个选项，但不支持 " *折叠到定义* " 命令。
