---
title: 旧版语言服务 Features1 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework]
ms.assetid: a646e4f0-767d-4cd1-8e1a-9a2aa210a1b7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c1f2a4010529d3d9727ceb76d6a34f2cbc41b959
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238473"
---
# <a name="legacy-language-service-features-1"></a>旧版语言服务功能1
管理包框架 (MPF) 语言服务可以支持一个或多个 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 功能，例如语法突出显示、IntelliSense 和断点验证。 每个功能都可以独立于其他功能来实现，但除语法突出显示之外，还需要一个分析器和一个扫描程序，这只需要一个扫描程序。

## <a name="in-this-section"></a>本节内容
- [旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

 描述支持语言对匹配所需的内容，也称为大括号匹配。

- [在旧版语言服务中注释代码](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

 描述支持所选代码的注释和取消注释所需的内容。

- [在旧版语言服务中自定义文档属性](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

 介绍支持嵌入到源文件中的文档属性所需的内容。

- [旧版语言服务中的大纲显示](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

 介绍通过实现隐藏区域来支持大纲所需满足的条件。

- [在旧版语言服务中重新格式化代码](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

 描述支持重新格式化代码所需的内容。

- [旧版语言服务中的代码片段支持](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

 描述支持代码段所需的内容，代码片段是插入并可以编辑的代码段。

- [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

 介绍支持 IntelliSense 参数信息操作以在类型化方法时显示方法签名所需的内容。

- [旧版语言服务中的快速信息](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

 介绍支持 IntelliSense 快速信息操作所需的内容，以便显示有关标识符的信息。

- [旧版语言服务中的成员完成](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

 介绍为了从列表中选择命名空间的成员，支持 IntelliSense 成员完成操作所需的内容。

- [旧版语言服务中的文字完成](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

 介绍支持用于完成部分键入的单词的 IntelliSense 完成单词操作所需的内容。

- [旧版语言服务中的自动窗口支持](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

 描述在您进行调试时，语言服务可为支持 **自动窗口提供** 哪些功能。

- [旧版语言服务中的导航栏支持](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

 介绍如何在编辑器视图的顶部使用 **导航栏** ，以便快速导航到该视图中显示的文件中的任何类型或成员。

- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

 描述支持源代码语法突出显示所需的内容。

- [验证旧版语言服务中的断点](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

 描述语言服务可执行哪些操作来支持在调试器外部验证断点。

## <a name="related-sections"></a>相关章节
- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 描述实现使用托管包框架的语言服务的所有功能所需的分析器和扫描程序。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 介绍使用 MPF 实现语言服务所需的内容。

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)

 描述使用注册基于 MPF 的语言服务所需的步骤 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [使用 IntelliSense](../../ide/using-intellisense.md)

 说明 IntelliSense 如何使语言引用易于访问。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)

 提供有关如何使用托管包框架 (MPF) 在托管代码中实现全功能语言服务的信息。
