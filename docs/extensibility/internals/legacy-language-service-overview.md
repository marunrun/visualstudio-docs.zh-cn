---
title: 传统语言服务概述 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], about language services
ms.assetid: bb44e27b-d228-463c-b2cf-cd5c24c7c1b5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aed653ec200063e72434fc758c7920e6caabafe1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707362"
---
# <a name="legacy-language-service-overview"></a>旧版语言服务概述
语言服务提供编辑器支持，使您能够实现某些[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]功能。 托管包框架 （MPF） 语言服务类提供对常用功能的完全支持，并支持其他功能。

## <a name="fully-supported-features-in-the-mpf"></a>强积金中完全支持的功能
 MPF 语言服务类支持以下功能：

- 语法突出显示

- 大纲显示

- 注释代码块

- 大括号匹配

- 代码片段

- 自定义文档属性

- IntelliSense 参数信息

- 感知快速信息

- IntelliSense 会员完成

- IntelliSense 字完成

## <a name="partially-supported-features-in-the-mpf"></a>强积金中部分支持的功能
 MPF 仅对以下功能提供部分支持。 这意味着您必须实现 MPF 调用的方法。

- 重新格式化代码。 提供实现重新格式化的代码。

- 通过标识有效的代码范围验证断点。 提供标识代码范围的代码。

- 支持调试器**自动**窗口以显示变量。 提供确定在窗口中显示内容的代码。

- 支持**导航栏**，用于类型和成员之间的快速导航。 实现并返回一个帮助程序类，该类填充**导航栏**组合框中的列表。

## <a name="implementation"></a>实现
 您必须完成几个步骤，以实现语言服务本身和要支持的语言服务功能。 这些步骤在以下主题中讨论：

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)

- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

- [旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

- [旧版语言服务中的大纲显示](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

- [在旧版语言服务中注释代码](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

- [在旧版语言服务中重新格式化代码](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

- [在旧版语言服务中自定义文档属性](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

- [旧版语言服务中的代码片段支持](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

- [旧版语言服务中的导航栏支持](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

- [旧版语言服务中的文字完成](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

- [旧版语言服务中的成员完成](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

- [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

- [旧版语言服务中的快速信息](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

- [旧版语言服务中的自动窗口支持](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

- [验证旧版语言服务中的断点](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

## <a name="see-also"></a>请参阅
- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [旧版语言服务扩展性](../../extensibility/internals/legacy-language-service-extensibility.md)
