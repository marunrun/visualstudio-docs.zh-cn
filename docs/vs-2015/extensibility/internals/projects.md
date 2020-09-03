---
title: 项目 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- custom tools [Visual Studio SDK]
- project subtypes [Visual Studio SDK]
- projects [Visual Studio SDK]
- project types [Visual Studio SDK]
ms.assetid: 237742e4-a638-4d5b-a9b3-6a69d627763c
caps.latest.revision: 44
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a251af12ccf4be5f0f48f789ac59fedaed3299b0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68183937"
---
# <a name="projects"></a>项目
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在 Visual Studio 中，项目是开发人员用来组织 **解决方案资源管理器**中显示的源代码文件和其他资源的容器。 通常，项目是文件 (例如，c # 项目的 .csproj 文件) 用于存储对源代码文件和资源（如位图文件）的引用。 项目使你可以组织、构建、调试和部署源代码，引用 Web 服务和数据库以及其他资源。 Vspackage 可以通过以下三种主要方式扩展 Visual Studio 项目系统： *项目类型*、 *项目子类型*和 *自定义工具*。  
  
## <a name="in-this-section"></a>本节内容  
 [项目类型](../../extensibility/internals/project-types.md)  
 *项目类型* 添加了对新类型的项目（如编程语言）的支持。 例如，Visual Studio 支持的每种语言都有其自己的项目类型，IronPython 集成示例包含 IronPython 语言的项目类型。 您必须为 c # 或 Visual Basic 以外的语言创建项目类型，以自定义项目在 **解决方案资源管理器**中的生成、调试、部署和显示方式。 有关详细信息，请参阅 [项目类型](../../extensibility/internals/project-types.md)。  
  
 [项目子类型](../../extensibility/internals/project-subtypes.md)  
 *项目子类型* 基于项目类型，可用于自定义项目的生成、调试和部署方式。 Visual Studio 将项目子类型用于智能设备项目;它们通过将新生成的程序从开发计算机复制到目标设备来自定义部署。 C # 和 Visual Basic 项目类型可用作项目子类型的基础;C + + 项目类型不能。 您自己的项目类型也可以用作项目子类型的基础。 有关详细信息，请参阅 [项目子类型](../../extensibility/internals/project-subtypes.md)。  
  
 [Web 项目](../../extensibility/internals/web-projects.md)  
 介绍 Web 项目，该项目将创建 Web 应用程序。  
  
 [新项目生成：](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md) 在幕后、第1部分和 [新项目生成：](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)  
 说明创建新项目时实际发生的情况。  
  
 [VSSDK 示例](../../misc/vssdk-samples.md)  
 介绍处理项目和解决方案的 VSSDK 中的示例。  
  
## <a name="related-sections"></a>相关章节  
 [深入探究 Visual Studio SDK](../../extensibility/internals/inside-the-visual-studio-sdk.md)  
 说明 Visual Studio 扩展性的不同方面。
