---
title: 在 MSBuild 项目文件中保留数据 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project files, persisting data in
ms.assetid: 6a920cb7-453d-4ffd-af1c-6f3084bd03f7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e83526007f676ae94ddce57936b627bcb4308c2a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706695"
---
# <a name="persisting-data-in-the-msbuild-project-file"></a>保留 MSBuild 项目文件中的数据
项目子类型可能需要将特定于子类型的数据保存到项目文件中，以便以后使用。 项目子类型使用项目文件持久性来满足以下要求：

1. 作为生成项目的一部分的持久化数据。 （有关 Microsoft 构建引擎的详细信息，请参阅[MSBuild](../../msbuild/msbuild.md).）与生成相关的信息可以：

    1. 与配置无关的数据。 也就是说，存储在 MSBuild 元素中的数据处于空白或缺失状态。

    2. 与配置相关的数据。 也就是说，存储在 MSBuild 元素中的数据是特定项目配置的条件。 例如：

        ```
        <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
        ```

2. 与生成无关的持久化数据。 此数据可以以非针对 XML 架构验证的自由格式 XML 表示。

    1. 与配置无关的数据。

    2. 与配置相关的数据。

## <a name="persisting-build-related-information"></a>持久化与生成相关的信息
 对构建项目有用的数据的持久性通过 MSBuild 进行处理。 MSBuild 系统维护生成相关信息的主表。 项目子类型负责访问此数据以获取和设置属性值。 项目子类型还可以通过添加要保留的其他属性和删除属性来增强与生成相关的数据表，以便不持久化这些属性。

 要修改 MSBuild 数据，项目子类型负责通过 从基础项目系统检索 MSBuild 属性对象<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>是在核心项目系统上实现的接口，通过运行`QueryInterface`来聚合项目子类型查询。

 以下过程概述了使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>删除 属性的步骤。

#### <a name="to-remove-a-property-from-an-msbuild-project-file"></a>从 MSBuild 项目文件中删除属性

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>调用`QueryInterface`项目子类型。

2. 使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.RemoveProperty%2A>`pszPropName`设置为要删除的属性进行调用。

### <a name="persisting-non-build-related-information"></a>保留非生成相关信息
 项目文件中重要的数据持久性并不重要，通过<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>处理。

 您可以在主<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>`project subtype aggregator`对象、`project subtype project configuration`对象或两者上实现。

 以下几点概述了有关非构建相关信息持久性的主要概念。

- 基本项目调用主项目子类型（即最外层项目子类型）聚合器对象来加载和保存配置独立数据，并调用项目子类型项目配置对象来加载或保存与配置相关的数据。

- 基本项目调用每个级别的项目子<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>类型聚合的多次方法，并传递每个级别的 GUID。

- 基本项目传递或接收专用于特定项目子类型的 XML 片段，并使用此机制作为在聚合级别之间持久状态的一种方式。

- 基项目调用最外层项目子类型在 GUID 中传递的<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>实现。 如果 GUID 属于最外层的项目子类型，它将处理调用本身;如果 GUID 属于最外层的项目子类型，则处理调用本身。否则，它将调用委托给内部项目子类型，等等，直到找到 GUID 对应的项目子类型。

- 项目子类型还可以在将调用委托给内部项目子类型之前或之后修改 XML 片段。 下面的示例显示了项目文件的摘录，其中包含特定于项目子类型的属性的文件的名称将传递给该项目子类型。

    ```
    <ProjectExtensions>
        <VisualStudio>
          <FlavorProperties GUID="{<FlavorGUID>}">
            <FlavorProject TestFileFolder="TestFile" />
          </FlavorProperties>
        </VisualStudio>
      </ProjectExtensions>
    ```

## <a name="see-also"></a>请参阅
- [项目子类型](../../extensibility/internals/project-subtypes.md)
