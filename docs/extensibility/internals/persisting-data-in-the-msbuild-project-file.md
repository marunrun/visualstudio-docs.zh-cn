---
title: 在 MSBuild 项目文件中保留数据 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project files, persisting data in
ms.assetid: 6a920cb7-453d-4ffd-af1c-6f3084bd03f7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7772f633c44c50b24995b7cc8a3f2f8bbbb01863
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72726051"
---
# <a name="persisting-data-in-the-msbuild-project-file"></a>保留 MSBuild 项目文件中的数据
项目子类型可能需要将特定于子类型的数据保存到项目文件中供以后使用。 项目子类型使用项目文件暂留满足以下要求：

1. 保留用作生成项目的一部分的数据。 （有关 Microsoft 生成引擎的详细信息，请参阅[MSBuild](../../msbuild/msbuild.md)。）与生成相关的信息可以：

    1. 独立于配置的数据。 也就是说，存储在具有空白或缺失条件的 MSBuild 元素中的数据。

    2. 依赖于配置的数据。 也就是说，存储在可用于特定项目配置的 MSBuild 元素中的数据。 例如:

        ```
        <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
        ```

2. 保存与生成无关的数据。 此数据可以用不根据 XML 架构验证的自由格式 XML 来表示。

    1. 独立于配置的数据。

    2. 依赖于配置的数据。

## <a name="persisting-build-related-information"></a>保持与生成相关的信息
 用于生成项目的数据的持久性是通过 MSBuild 处理的。 MSBuild 系统维护与生成相关的信息的主表。 项目子类型负责访问此数据以获取和设置属性值。 项目子类型还可以通过添加要保存的附加属性和通过删除属性使其不会被保留，从而增加与生成相关的数据表。

 为了修改 MSBuild 数据，项目子类型负责通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 从基本项目系统检索 MSBuild 属性对象。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 是在核心项目系统中实现的接口，并且通过运行 `QueryInterface`，对其进行聚合项目子类型查询。

 下面的过程概述了使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 删除属性的步骤。

#### <a name="to-remove-a-property-from-an-msbuild-project-file"></a>从 MSBuild 项目文件中删除属性

1. 对项目子类型的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 调用 `QueryInterface`。

2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.RemoveProperty%2A>，并将 `pszPropName` 设置为要删除的属性。

### <a name="persisting-non-build-related-information"></a>保持非生成相关的信息
 不重要的项目文件中的数据持久性会通过 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 进行处理。

 可以在主 `project subtype aggregator` 对象、`project subtype project configuration` 对象或两者上实现 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>。

 以下要点概述了与非生成相关信息的持久性有关的主要概念。

- 基本项目对主项目子类型（即，最外面的项目子类型）聚合器对象调用以加载和保存配置独立数据，并对项目子类型项目配置对象调用以加载或保存依赖配置数据.

- 基本项目将为每个级别的项目子类型聚合调用多次 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 方法，并传递每个级别的 GUID。

- 基本项目传递或接收专用于特定项目子类型的 XML 片段，并使用此机制作为在聚合级别之间保持状态的方式。

- 基本项目调用最外面的项目子类型的 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>implementation 传入 GUID。 如果 GUID 属于最外面的项目子类型，它将处理调用本身;否则，它会将调用委托给内部项目子类型，依此类推，直到找到 GUID 对应的项目子类型。

- 项目子类型还可以在将调用委托给内部项目子类型之前或之后修改 XML 片段。 下面的示例演示了项目文件的摘录，其中包含特定于项目子类型的属性的文件的名称将传递给该项目子类型。

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