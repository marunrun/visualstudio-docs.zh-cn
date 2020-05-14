---
title: 传统语言服务功能1 |微软文档
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
ms.openlocfilehash: f0be7cb4401792b30eac595faf64162dc375dbb2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707397"
---
# <a name="legacy-language-service-features"></a>旧版语言服务功能
托管包框架 （MPF） 语言服务可以支持一个或多个[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]功能，如语法突出显示、IntelliSense 和断点验证。 每个功能都可以独立于其他功能实现，但除了语法突出显示（只需要扫描仪）外，所有功能都需要解析器和扫描仪。

## <a name="in-this-section"></a>本节内容
- [旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

 描述支持语言对匹配（也称为大括号匹配）所需的内容。

- [在旧版语言服务中注释代码](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

 描述支持注释和取消注释所选代码所需的内容。

- [在旧版语言服务中自定义文档属性](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

 描述支持嵌入在源文件中的文档属性所需的内容。

- [旧版语言服务中的大纲显示](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

 描述通过实施隐藏区域来支持大纲的内容。

- [在旧版语言服务中重新格式化代码](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

 描述支持重新格式化代码所需的内容。

- [旧版语言服务中的代码片段支持](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

 描述支持代码段所需的内容，这些代码段是插入并可编辑的代码段。

- [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

 描述在键入方法时支持 IntelliSense 参数信息操作以显示方法签名所需的内容。

- [旧版语言服务中的快速信息](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

 描述支持 IntelliSense 快速信息操作以显示有关标识符信息所需的内容。

- [旧版语言服务中的成员完成](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

 描述支持从列表中选择命名空间成员所需的"IntelliSense 成员完成"操作所需的内容。

- [旧版语言服务中的文字完成](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

 描述支持"IntelliSense 完整字"操作以完成部分键入的单词所需的内容。

- [旧版语言服务中的自动窗口支持](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

 描述在调试时，语言服务可以采取哪些功能来支持**自动窗口**。

- [旧版语言服务中的导航栏支持](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

 描述如何使用编辑器视图顶部的**导航栏**向该视图中显示的文件中的任何类型的或成员提供快速导航。

- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

 描述支持源代码的语法突出显示所需的内容。

- [验证旧版语言服务中的断点](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

 描述语言服务可以做些什么来支持验证调试器外的断点。

## <a name="related-sections"></a>相关章节
- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 描述实现使用托管包框架的语言服务的所有功能所需的解析器和扫描仪。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 描述使用 MPF 实现语言服务所需的内容。

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)

 描述向[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]注册基于 MPF 的语言服务所需的步骤。

- [Using IntelliSense](../../ide/using-intellisense.md)

 解释 IntelliSense 如何让语言参考易于访问。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)

 提供有关如何使用托管包框架 （MPF） 在托管代码中实现全功能语言服务的信息。
