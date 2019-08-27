---
title: 旧版语言服务概述 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], about language services
ms.assetid: bb44e27b-d228-463c-b2cf-cd5c24c7c1b5
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c5964aa82d76791d29313ac787f1216c9c9ad283
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202715"
---
# <a name="legacy-language-service-overview"></a>旧版语言服务概述
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

语言服务都会提供使您可以实现特定的编辑器支持[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]功能。 托管包框架 (MPF) 语言服务类提供完全支持对常用功能和对其他功能的部分支持。  
  
## <a name="fully-supported-features-in-the-mpf"></a>MPF 中完全支持的功能  
 MPF 语言服务类支持以下功能：  
  
- 语法突出显示  
  
- 大纲显示  
  
- 注释的代码块  
  
- 大括号匹配  
  
- 代码片段  
  
- 自定义文档属性  
  
- IntelliSense 参数信息  
  
- IntelliSense 快速信息  
  
- IntelliSense 成员完成  
  
- IntelliSense 文字自动完成  
  
## <a name="partially-supported-features-in-the-mpf"></a>MPF 中部分支持的功能  
 MPF 提供以下功能仅部分支持。 这意味着您必须实现的 MPF 调用的方法。  
  
- 重新格式化代码。 提供用于实现重新格式化操作的代码。  
  
- 通过标识有效的代码来验证断点跨越。 提供的代码，用于标识代码范围。  
  
- 支持调试器**自动**显示变量的窗口。 提供确定如何在窗口中显示的代码。  
  
- 支持**导航栏**类型和成员之间快速导航。 实现并返回填充的列表中的帮助器类**导航栏**组合框。  
  
## <a name="implementation"></a>实现  
 必须完成几个步骤来实现本身的语言服务和你想要为您的语言支持的语言服务功能。 以下主题中讨论了这些步骤：  
  
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
 [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)   
 [旧版语言服务扩展性](../../extensibility/internals/legacy-language-service-extensibility.md)
