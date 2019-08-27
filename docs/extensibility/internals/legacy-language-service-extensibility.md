---
title: 旧版语言服务扩展性 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services
- Visual Studio, language services
ms.assetid: 2700cd4d-5f68-43fc-b62f-dc80c3f3aa85
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 14bee804d532138ddf5c9b63039f4bfb8abbe02c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344832"
---
# <a name="legacy-language-service-extensibility"></a>旧版语言服务扩展性
语言服务提供用于编辑在 IDE 中的源代码的特定于语言的支持。

 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要了解有关实现语言服务的新方法的详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

 本部分讨论的结构和旧版语言服务实现。

## <a name="in-this-section"></a>本节内容
- [迁移旧版语言服务](../../extensibility/internals/migrating-a-legacy-language-service.md)

 介绍如何更新到最新版本从 Visual Studio 2008 语言服务。

- [旧版语言服务基础知识](../../extensibility/internals/legacy-language-service-essentials.md)

 提供有关如何开发语言服务集成到 Visual Studio 中，一种编程语言的重要信息。

- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)

 提供可帮助您创建语言服务主题的链接。

- [在旧版语言服务中进行语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 提供了支持语法突出显示语言服务中的信息。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)

 提供有关如何使用托管的包框架 (MPF) 在托管代码中实现完备语言服务的信息。

- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)

 介绍了库和工具，您可以浏览在 IDE 中的符号的树视图。

## <a name="related-sections"></a>相关章节
- [编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)

 概述 Visual Studio 编辑器。

- [用于调试的语言服务支持](../../extensibility/internals/language-service-support-for-debugging.md)

 提供有关的信息和链接到 Visual Studio 调试 SDK，其中包含创建和自定义调试器组件用于调试的程序所需的信息。