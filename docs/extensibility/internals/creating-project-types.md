---
title: 创建项目类型 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, new
- projects [Visual Studio SDK], new project types
ms.assetid: bdb2d22e-d622-450c-bb2d-98152a745fcf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 005765cb66a23f2efcf0c8defb323120d79bef60
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66314565"
---
# <a name="create-project-types"></a>创建项目类型
您可以扩展[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]通过创建新的项目类型。 若要创建新的项目类型，必须了解的几个概念，并完成一系列步骤。 以下主题提供如何创建项目类型的概述。

## <a name="in-this-section"></a>本节内容
- [项目类型设计决策](../../extensibility/internals/project-type-design-decisions.md)

 讨论项目、 项目文件持久性，以及必须在创建新的项目类型之前做出的承诺的机修工保养设计决策。

- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)

 概述创建支持编辑代码和编译、 生成、 调试和部署你的项目中的应用程序等编程任务的新项目类型时必须遵循的步骤。

- [使用项目工厂创建的项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)

 提供有关如何提供和使用项目工厂来创建新项目的实例的信息。

- [注册项目类型](../../extensibility/internals/registering-a-project-type.md)

 提供语句从注册表，以提供默认路径和数据，以及一个表包含每个语句的注册表脚本中的条目的代码的示例。

- [项目持久性](../../extensibility/internals/project-persistence.md)

 介绍如何使用`IPersistFileFormat`来持久保存文件和不基于文件的项目对象。

- [使用 MSBuild](../../extensibility/internals/using-msbuild.md)

 介绍如何使用您的项目类型[!INCLUDE[vstecmsbuild](../../extensibility/internals/includes/vstecmsbuild_md.md)]生成引擎以使用户可以从生成[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和在命令行。

## <a name="related-sections"></a>相关章节
- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)

 介绍代码如查看工具的体系结构**对象浏览器**并**类视图**窗口。 描述的接口和方法，用于在 VSPackage 中实现对象浏览。

- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)

 讨论在确定使用哪个编辑器打开项目项时播放项目的重要性和可以对操作项目资源的方法。

- [使用 Windows Installer 安装 Vspackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)

 演示如何为你的 VSPackage 提供其自己唯一的标识以及如何将你的 VSPackage Dll 和其他信息包装在一个 Windows Installer 程序包 ( *。MSI*文件) 以部署到你的客户。

- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)

 描述如何[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]视图和地址的层次结构。

- [VSPackage](../../extensibility/internals/vspackages.md)

 提供的 VSPackage，扩展了一个可安装的 COM 对象概述[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]环境，并讨论了如何实现你自己的 VSPackage。

- [项目类型](../../extensibility/internals/project-types.md)

 讨论如何使用项目来修改代码，编译和生成代码，并运行和调试代码，并提供有关如何创建项目类型的详细主题的链接。