---
title: 在 MSBuild 项目文件中保留数据 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project files, persisting data in
ms.assetid: 6a920cb7-453d-4ffd-af1c-6f3084bd03f7
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 39d2ab449c3623a90dd76729b46a9f353900fc88
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704122"
---
# <a name="persisting-data-in-the-msbuild-project-file"></a>保留 MSBuild 项目文件中的数据
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目子类型可能需要将特定于子类型的数据保存到项目文件中供以后使用。 项目子类型使用项目文件暂留满足以下要求：  
  
1. 保留用作生成项目的一部分的数据。  (有关 Microsoft 生成引擎的详细信息，请参阅 [MSBuild](https://msdn.microsoft.com/7c49aba1-ee6c-47d8-9de1-6f29a906e20b)。 ) 与生成相关的信息可以：  
  
    1. 独立于配置的数据。 也就是说，存储在具有空白或缺失条件的 MSBuild 元素中的数据。  
  
    2. 依赖于配置的数据。 也就是说，存储在可用于特定项目配置的 MSBuild 元素中的数据。 例如：  
  
        ```  
        <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">  
        ```  
  
2. 保存与生成无关的数据。 此数据可以用不根据 XML 架构验证的自由格式 XML 来表示。  
  
    1. 独立于配置的数据。  
  
    2. 依赖于配置的数据。  
  
## <a name="persisting-build-related-information"></a>保持与生成相关的信息  
 用于生成项目的数据的持久性是通过 MSBuild 处理的。 MSBuild 系统维护与生成相关的信息的主表。 项目子类型负责访问此数据以获取和设置属性值。 项目子类型还可以通过添加要保存的附加属性和通过删除属性使其不会被保留，从而增加与生成相关的数据表。  
  
 为了修改 MSBuild 数据，项目子类型负责通过从基本项目系统中检索 MSBuild 属性对象 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 是在核心项目系统中实现的接口，并且通过运行对其执行聚合项目子类型查询 `QueryInterface` 。  
  
 下面的过程概述了使用删除属性的步骤 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 。  
  
#### <a name="to-remove-a-property-from-an-msbuild-project-file"></a>从 MSBuild 项目文件中删除属性  
  
1. 对 `QueryInterface` <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 项目子类型调用。  
  
2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.RemoveProperty%2A> ，并 `pszPropName` 将设置为要删除的属性。  
  
### <a name="persisting-non-build-related-information"></a>保持非生成相关的信息  
 对于不重要的项目文件中的数据的持久性是通过处理的 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 。  
  
 可以 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 在主 `project subtype aggregator` 对象和 `project subtype project configuration` /或对象上实现。  
  
 以下要点概述了与非生成相关信息的持久性有关的主要概念。  
  
- 基本项目对主项目子类型进行调用， (即，最外面的项目子类型) 聚合器对象加载和保存配置独立的数据，并在项目子类型项目配置对象上调用来加载或保存依赖于配置的数据。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>对于每个级别的项目子类型聚合，基项目将多次调用方法，并传递每个级别的 GUID。  
  
- 基本项目传递或接收专用于特定项目子类型的 XML 片段，并使用此机制作为在聚合级别之间保持状态的方式。  
  
- 基本项目调用在 GUID 中传递的最外面的项目子类型 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 实现。 如果 GUID 属于最外面的项目子类型，它将处理调用本身;否则，它会将调用委托给内部项目子类型，依此类推，直到找到 GUID 对应的项目子类型。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [项目子类型](../../extensibility/internals/project-subtypes.md)
