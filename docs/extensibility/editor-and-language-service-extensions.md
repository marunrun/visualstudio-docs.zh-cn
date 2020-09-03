---
title: 编辑器和语言服务扩展 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80712025"
---
# <a name="editor-and-language-service-extensions"></a>编辑器和语言服务扩展
可以扩展 Visual Studio 代码编辑器的大多数功能。 该编辑器基于 (WPF) Windows Presentation Foundation，并用托管代码编写。 尽管此设计与 Visual Studio 早期版本中的设计不同，但它提供了大多数相同的功能。 若要扩展编辑器，请使用 (MEF) Managed Extensibility Framework。

 Visual Studio SDK 提供了称为 *填充* 程序的适配器，以支持为早期版本编写的 vspackage。 尽管如此，如果你有现有的 VSPackage，我们建议你将其更新为新技术，以获得更好的性能和可靠性。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)|使用编辑器项模板的简介。|
|[扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)|指向介绍核心编辑器设计和功能的文档的链接，并演示如何对其进行扩展。|
|[编辑器中的旧接口](/visualstudio/extensibility/legacy-interfaces-in-the-editor?view=vs-2015)|说明如何从现有代码访问核心编辑器的文档链接。|
|[创建自定义编辑器和设计器](../extensibility/creating-custom-editors-and-designers.md)|说明如何创建自定义编辑器的文档的链接。|
|[旧版语言服务扩展性](../extensibility/internals/legacy-language-service-extensibility.md)|介绍如何将编程语言集成到 Visual Studio 的文档的链接。|
|[Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)|介绍 (MEF) Managed Extensibility Framework。|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|介绍 WPF)  (Windows Presentation Foundation。|
