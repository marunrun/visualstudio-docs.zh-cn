---
title: 项目 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- custom tools [Visual Studio SDK]
- project subtypes [Visual Studio SDK]
- projects [Visual Studio SDK]
- project types [Visual Studio SDK]
ms.assetid: 237742e4-a638-4d5b-a9b3-6a69d627763c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6b7a9299321d2aa80eebb564bf9b926f07ab0108
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706218"
---
# <a name="projects"></a>项目
在 Visual Studio 中，项目是开发人员用来组织源代码文件以及**解决方案资源管理器**中显示的其他资源的容器。 通常，项目是文件（例如，C# 项目的 .csproj 文件），用于存储对源代码文件和资源（如位图文件）的引用。 项目允许您组织、构建、调试和部署源代码、对 Web 服务和数据库的引用以及其他资源。 VS包可以通过三种主要方式扩展 Visual Studio 项目系统：*项目类型*、*项目子类型*和*自定义工具*。

## <a name="in-this-section"></a>本节内容
- [项目类型](../../extensibility/internals/project-types.md)

 *项目类型*增加了对新类型的项目（如编程语言）的支持。 例如，Visual Studio 支持的每种语言都有自己的项目类型，IronPython 集成示例包括 IronPython 语言的项目类型。 您必须为 C# 或 Visual Basic 以外的语言创建项目类型，以自定义**如何在解决方案资源管理器**中生成、调试、部署和显示项目。 有关详细信息，请参阅[项目类型](../../extensibility/internals/project-types.md)。

- [项目子类型](../../extensibility/internals/project-subtypes.md)

 *项目子类型*基于项目类型，可用于自定义项目的生成、调试和部署方式。 Visual Studio 使用智能设备项目的项目子类型;他们通过将新构建的程序从开发计算机复制到目标设备来自定义部署。 C# 和可视化基本项目类型可用作项目子类型的基础;C++项目类型不能。 您自己的项目类型也可以用作项目子类型的基础。 有关详细信息，请参阅[项目子类型](../../extensibility/internals/project-subtypes.md)。

- [Web 项目](../../extensibility/internals/web-projects.md)

 解释 Web 项目，而 Web 项目又创建 Web 应用程序。

- [新项目生成：引擎盖下，第一部分](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)和[新项目生成：在引擎盖下，第二部分](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)

 说明创建新项目时实际发生的情况。

- [VSSDK 样本](https://github.com/Microsoft/VSSDK-Extensibility-Samples)包含 VSSDK 中处理项目和解决方案的示例。

## <a name="related-sections"></a>相关章节
- [深入探究 Visual Studio SDK](../../extensibility/internals/inside-the-visual-studio-sdk.md)

 解释可视化工作室扩展性的不同方面。
