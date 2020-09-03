---
title: 自定义工具 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, custom tools
- tools [Visual Studio], custom
- custom tools
ms.assetid: d669f154-9b23-48b6-b9f6-7419c8dd61a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e60f1d8cb8b25ed50b0b20c5ebb538286687ad72
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708950"
---
# <a name="custom-tools"></a>自定义工具
*自定义工具* 使你可以将工具与项目中的项相关联，并在每次保存文件时运行该工具。 某些自定义工具（有时称为 *单文件生成器*）经常用于实现从数据生成代码的转换器，反之亦然。 例如，单文件生成器会创建 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 和源代码，并将其放 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 在 *. 设置* 和 *.resx* 文件中。 生成的源代码提供对 *设置* 和 *.resx* 文件中的数据的强类型访问。 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]和 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目类型支持自定义工具; [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 项目类型不支持。 你自己的项目类型还可以支持自定义工具。

 自定义工具是实现接口的已注册组件 `IVsSingleFileGenerator` 。

 自定义工具与 `ProjectItem` interface 对象相关联，并且与设计器和编辑器类似。 自定义工具使用由表示的文件 `ProjectItem` 作为输入，并写入一个新文件，其文件名由 `DefaultExtension` 方法提供。

## <a name="in-this-section"></a>本节内容
- [实现单文件生成器](../../extensibility/internals/implementing-single-file-generators.md)

 描述如何使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 接口实现自定义工具。

- [注册单个文件生成器](../../extensibility/internals/registering-single-file-generators.md)

 提供自定义工具的所有注册表项的说明。

- [向可视化设计器公开类型](../../extensibility/internals/exposing-types-to-visual-designers.md)

 介绍项目系统如何为可视化设计器提供支持，以便通过临时可执行文件 (PE) 文件访问生成的类和类型。

- [保留项目项的属性](../../extensibility/persisting-the-property-of-a-project-item.md)

 演示如何在项目文件中保存项目项属性，如源文件的作者。

## <a name="reference"></a>参考
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 提供有关的详细信息，该信息将 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 单个输入文件转换为单个输出文件，该文件可编译或添加到项目。

 <xref:EnvDTE.ProjectItem> 介绍 `ProjectItem` 接口，它表示项目中的项。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> 提供有关方法的详细信息 `DefaultExtension` ，该方法检索为输出文件名提供的文件扩展名。

## <a name="related-sections"></a>相关章节
- [扩展项目](../../extensibility/extending-projects.md)

 介绍如何使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目和解决方案来组织代码文件和资源文件，以及如何实现源代码管理。
