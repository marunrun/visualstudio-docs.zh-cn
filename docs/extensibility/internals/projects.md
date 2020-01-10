---
title: 项目 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- custom tools [Visual Studio SDK]
- project subtypes [Visual Studio SDK]
- projects [Visual Studio SDK]
- project types [Visual Studio SDK]
ms.assetid: 237742e4-a638-4d5b-a9b3-6a69d627763c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bfe172d0255a6874d65fb940afd0f6f0beb1657a
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75848794"
---
# <a name="projects"></a>项目
在 Visual Studio 中，项目是开发人员用来组织**解决方案资源管理器**中显示的源代码文件和其他资源的容器。 通常，项目是存储对源代码文件和资源（如位图文件） C#的引用的文件（例如，项目的 .csproj 文件）。 项目使你可以组织、构建、调试和部署源代码，引用 Web 服务和数据库以及其他资源。 Vspackage 可以通过以下三种主要方式扩展 Visual Studio 项目系统：*项目类型*、*项目子类型*和*自定义工具*。

## <a name="in-this-section"></a>本节内容
- [项目类型](../../extensibility/internals/project-types.md)

 *项目类型*添加了对新类型的项目（如编程语言）的支持。 例如，Visual Studio 支持的每种语言都有其自己的项目类型，IronPython 集成示例包含 IronPython 语言的项目类型。 您必须为C#或 Visual Basic 以外的其他语言创建项目类型，以自定义项目在**解决方案资源管理器**中的生成、调试、部署和显示方式。 有关详细信息，请参阅[项目类型](../../extensibility/internals/project-types.md)。

- [项目子类型](../../extensibility/internals/project-subtypes.md)

 *项目子类型*基于项目类型，可用于自定义项目的生成、调试和部署方式。 Visual Studio 将项目子类型用于智能设备项目;它们通过将新生成的程序从开发计算机复制到目标设备来自定义部署。 C#和 Visual Basic 项目类型可用作项目子类型的基础;C++项目类型不能为。 您自己的项目类型也可以用作项目子类型的基础。 有关详细信息，请参阅[项目子类型](../../extensibility/internals/project-subtypes.md)。

- [Web 项目](../../extensibility/internals/web-projects.md)

 介绍 Web 项目，该项目将创建 Web 应用程序。

- [新项目生成：](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)在幕后、第1部分和[新项目生成：](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)

 说明创建新项目时实际发生的情况。

- [VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)包含处理项目和解决方案的 VSSDK 中的示例。

## <a name="related-sections"></a>相关章节
- [Visual Studio SDK 内](../../extensibility/internals/inside-the-visual-studio-sdk.md)

 说明 Visual Studio 扩展性的不同方面。
