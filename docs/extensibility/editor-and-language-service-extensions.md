---
title: 编辑器和语言服务扩展 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK]
ms.assetid: 5653bac9-724f-4948-a820-68ce6aa96365
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7e37165dc5fe9ac010545304218e807d923b424b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712025"
---
# <a name="editor-and-language-service-extensions"></a>编辑器和语言服务扩展
您可以扩展 Visual Studio 代码编辑器的大多数功能。 编辑器基于 Windows 演示基础 （WPF），以托管代码编写。 尽管此设计不同于早期版本的 Visual Studio 的设计，但它提供了大多数相同的功能。 要扩展编辑器，请使用托管扩展性框架 （MEF）。

 Visual Studio SDK 提供称为*hims*的适配器，以支持为早期版本编写的 VS 包。 但是，如果您有现有的 VSPackage，我们建议您将其更新到新技术，以获得更好的性能和可靠性。

## <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)|使用编辑器项模板的简介。|
|[扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)|指向文档的链接，这些文档介绍了核心编辑器的设计和功能，并演示如何扩展它。|
|[编辑器中的旧接口](/visualstudio/extensibility/legacy-interfaces-in-the-editor?view=vs-2015)|指向解释如何从现有代码访问核心编辑器的文档的链接。|
|[创建自定义编辑器和设计器](../extensibility/creating-custom-editors-and-designers.md)|指向解释如何创建自定义编辑器的文档的链接。|
|[传统语言服务可扩展性](../extensibility/internals/legacy-language-service-extensibility.md)|指向描述如何将编程语言集成到 Visual Studio 的文档的链接。|
|[Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)|介绍托管扩展性框架 （MEF）。|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|介绍 Windows 演示基础 （WPF）。|
