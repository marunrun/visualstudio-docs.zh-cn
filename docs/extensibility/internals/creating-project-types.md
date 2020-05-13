---
title: 创建项目类型 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, new
- projects [Visual Studio SDK], new project types
ms.assetid: bdb2d22e-d622-450c-bb2d-98152a745fcf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d2398b63b8cd52784252cfc764bb6c6a30e1accc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709071"
---
# <a name="create-project-types"></a>创建项目类型
您可以通过创建新项目[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]类型进行扩展。 要创建新的项目类型，必须了解多个概念并完成多个步骤。 以下主题概述了如何创建项目类型。

## <a name="in-this-section"></a>在本节中
- [项目类型设计决策](../../extensibility/internals/project-type-design-decisions.md)

 讨论在创建新项目类型之前必须做出的项目、项目文件持久性和承诺机制设计决策。

- [检查表：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)

 概述了创建支持编辑代码和编译、构建、调试和部署项目中应用程序等编程任务的新项目类型时必须遵循的步骤。

- [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)

 提供有关如何提供和使用项目工厂创建新项目实例的信息。

- [注册项目类型](../../extensibility/internals/registering-a-project-type.md)

 提供提供默认路径和数据的注册表中的语句的代码示例，以及包含每个语句注册表脚本中的条目的表。

- [项目持久性](../../extensibility/internals/project-persistence.md)

 讨论 使用`IPersistFileFormat`来保留文件和非基于文件的项目对象。

- [使用 MSBuild](../../extensibility/internals/using-msbuild.md)

 描述项目类型如何使用[!INCLUDE[vstecmsbuild](../../extensibility/internals/includes/vstecmsbuild_md.md)]生成引擎来允许用户从[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]命令行和命令行生成。

## <a name="related-sections"></a>相关章节
- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)

 解释代码查看工具（如**对象浏览器**和**类视图**窗口）的体系结构。 描述用于在 VSPackage 中实现对象浏览的接口和方法。

- [添加项目和项目项目模板](../../extensibility/internals/adding-project-and-project-item-templates.md)

 讨论项目在确定打开项目项时使用哪个编辑器以及如何操纵项目资源方面的重要性。

- [使用 Windows 安装程序安装 VS 包](../../extensibility/internals/installing-vspackages-with-windows-installer.md)

 演示如何为 VSPackage 提供其自己的唯一标识，以及如何在 Windows 安装程序包（中包装 VSPackage DLL 和其他信息 *）用于*部署到客户的 MSI 文件）。

- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)

 描述视图[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和地址层次结构的方式。

- [VSPackage](../../extensibility/internals/vspackages.md)

 提供 VSPackage 的概述，这是一个可安装的 COM[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]对象，可扩展环境并讨论如何实现自己的 VSPackage。

- [项目类型](../../extensibility/internals/project-types.md)

 讨论如何使用项目来修改代码、编译和生成代码以及运行和调试代码，并提供有关如何创建项目类型的详细主题的链接。
