---
title: 编辑器和语言服务扩展 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK]
ms.assetid: 5653bac9-724f-4948-a820-68ce6aa96365
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1df6f65db70425650fc2860bf5ddf6e2d2e203c6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353374"
---
# <a name="editor-and-language-service-extensions"></a>编辑器和语言服务扩展
您可以扩展 Visual Studio 代码编辑器中的大多数功能。 编辑器基于 Windows Presentation Foundation (WPF) 上，并以托管代码编写。 尽管这种设计不同于早期版本的 Visual Studio 中设计，它提供的大多数相同功能。 若要扩展编辑器，使用 Managed Extensibility Framework (MEF)。

 Visual Studio SDK 提供了名为适配器*填充程序*以支持为早期版本编写的 Vspackage。 不过，如果有现有的 VSPackage，我们建议对新技术，从而获得更好的性能和可靠性更新它。

## <a name="related-topics"></a>相关主题

|标题|描述|
|-----------|-----------------|
|[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)|介绍如何使用编辑器项模板。|
|[将编辑器和语言服务扩展](../extensibility/extending-the-editor-and-language-services.md)|引入的设计和功能的核心编辑器并演示如何对其进行扩展的文档的链接。|
|[在编辑器中的旧接口](../extensibility/legacy-interfaces-in-the-editor.md)|说明如何从现有代码访问核心编辑器文档的链接。|
|[创建自定义编辑器和设计器](../extensibility/creating-custom-editors-and-designers.md)|说明如何创建自定义编辑器的文档的链接。|
|[旧版语言服务扩展性](../extensibility/internals/legacy-language-service-extensibility.md)|介绍如何集成到 Visual Studio 编程语言的文档的链接。|
|[Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)|引入了 Managed 的 Extensibility Framework (MEF)。|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|引入了 Windows Presentation Foundation (WPF)。|