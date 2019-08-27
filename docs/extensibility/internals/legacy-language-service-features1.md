---
title: 旧版语言服务功能 1 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework]
ms.assetid: a646e4f0-767d-4cd1-8e1a-9a2aa210a1b7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b8fead42087699deb257b29093ee4349bbc8ef78
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333628"
---
# <a name="legacy-language-service-features"></a>旧版语言服务功能
托管的包框架 (MPF) 语言服务可以支持一个或多个[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]功能，如语法突出显示、 IntelliSense 和断点验证。 每个功能可以实现相互独立，但所有都需要一个分析器和除语法突出显示，这要求仅扫描程序扫描程序。

## <a name="in-this-section"></a>本节内容
- [旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

 介绍什么是支持语言对自动匹配，也称为大括号匹配。

- [在旧版语言服务中注释代码](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

 介绍什么是注释和取消注释所选代码的支持。

- [在旧版语言服务中自定义文档属性](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

 介绍什么是需要支持源代码文件中嵌入的文档属性。

- [旧版语言服务中的大纲显示](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

 介绍什么是支持通过实施的隐藏区域的大纲显示。

- [在旧版语言服务中重新格式化代码](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

 介绍什么是支持重格式化代码。

- [旧版语言服务中的代码片段支持](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

 介绍什么是需要支持代码段，一些代码片段的插入，可以进行编辑。

- [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

 介绍支持用于显示方法签名，方法是键入的参数的 IntelliSense 信息操作的要求。

- [旧版语言服务中的快速信息](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

 介绍什么是支持的 IntelliSense 快速信息操作用于显示有关标识符的信息。

- [旧版语言服务中的成员完成](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

 介绍什么支持从列表中选择一个命名空间的成员的成员的 IntelliSense 完成操作所必需。

- [旧版语言服务中的文字完成](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

 介绍支持用于完成未完全键入的单词智能感知完成单词操作的要求。

- [旧版语言服务中的自动窗口支持](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

 描述语言服务可以执行的操作以支持**自动**窗口进行调试时。

- [旧版语言服务中的导航栏支持](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

 介绍如何使用**导航栏**提供快速导航到任何类型或成员在该视图中显示的文件中的编辑器视图顶部...

- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

 介绍什么是需要支持语法突出显示的源代码。

- [验证旧版语言服务中的断点](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

 描述语言服务可以执行的操作以支持调试器外部验证断点。

## <a name="related-sections"></a>相关章节
- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 介绍了分析器和扫描程序所需实现使用托管的包框架的语言服务的所有功能。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 介绍什么是通过使用 MPF 实现语言服务所必需。

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)

 介绍的步骤所需注册一种基于 MPF 的语言服务，具有[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

- [使用 IntelliSense](../../ide/using-intellisense.md)

 介绍 IntelliSense 如何使语言参考可以轻松地访问。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)

 提供有关如何使用托管的包框架 (MPF) 在托管代码中实现完备语言服务的信息。