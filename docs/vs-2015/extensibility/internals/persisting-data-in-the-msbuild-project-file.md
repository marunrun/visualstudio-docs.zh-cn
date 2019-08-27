---
title: 将数据保留在 MSBuild 项目文件 |Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704122"
---
# <a name="persisting-data-in-the-msbuild-project-file"></a>保留 MSBuild 项目文件中的数据
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目子类型可能需要将特定于子类型的数据保存到项目文件以供将来使用。 项目子类型使用项目文件持久性来满足以下要求：  
  
1. 保存生成项目的过程中使用的数据。 (有关 Microsoft 生成引擎的详细信息，请参阅[MSBuild](https://msdn.microsoft.com/7c49aba1-ee6c-47d8-9de1-6f29a906e20b)。)可以与生成相关的信息：  
  
    1. 独立于配置的数据。 也就是说，空白或 missing 条件与 MSBuild 元素中存储的数据。  
  
    2. 依赖于配置的数据。 也就是说，限制为特定项目配置的 MSBuild 元素中存储的数据。 例如：  
  
        ```  
        <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">  
        ```  
  
2. 保留不相关，若要生成的数据。 此数据可以表示自由格式的 xml 中不根据 XML 架构验证。  
  
    1. 独立于配置的数据。  
  
    2. 依赖于配置的数据。  
  
## <a name="persisting-build-related-information"></a>保持与生成相关的信息  
 通过 MSBuild 处理持久性数据可用于生成项目。 MSBuild 系统会维护与生成相关的信息的主表。 项目子类型负责访问此数据来获取和设置属性值。 项目子类型还可以扩充与生成相关的数据表，通过添加其他属性保留和删除属性，以便它们不会保留。  
  
 若要修改的 MSBuild 数据，项目子类型负责检索 MSBuild 属性对象从基本项目系统通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 是通过运行为其实现的核心项目系统和聚合的项目子类型查询接口， `QueryInterface`。  
  
 以下过程概述了相应步骤删除属性使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>。  
  
#### <a name="to-remove-a-property-from-an-msbuild-project-file"></a>若要从一个 MSBuild 项目文件中删除属性  
  
1. 调用`QueryInterface`上<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>的项目子类型。  
  
2. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.RemoveProperty%2A>与`pszPropName`设置为你想要删除的属性。  
  
### <a name="persisting-non-build-related-information"></a>保持非生成相关的信息  
 通过处理的项目文件中并不重要生成的数据持久性<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>。  
  
 您可以实现<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>在主要`project subtype aggregator`对象，`project subtype project configuration`对象，或两者。  
  
 以下几点介绍有关与非生成相关信息的持久性的主要概念。  
  
- 对主项目子类型 （即，最外面的项目子类型） 聚合器对象加载和保存配置独立的数据，调用的基础项目和它调用上要加载或保存取决于配置的项目子类型项目配置对象数据。  
  
- 基础项目调用的方法<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>多个项目子类型聚合，每个级别的时间，并将传递每个级别的 GUID。  
  
- 基础项目通过或接收的 XML 片断，专用于特定项目子类型，并使用此机制作为一种方法之间的聚合级别保持状态。  
  
- 基础项目调用的最外层项目子类型<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>实现传入一个 GUID。 如果 GUID 属于最外面的项目子类型，它将处理的调用，然后重试。否则它将调用委托给内部项目子类型，依此类推，直到找到 GUID 对应的项目子类型。  
  
- 项目子类型还可以修改 XML 片段之前或之后它将调用委托给内部项目子类型。 下面的示例显示了一段摘录项目文件，其中包含特定于项目子类型，属性的文件的名称传递到该项目子类型。  
  
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
 [项目子类型](../../extensibility/internals/project-subtypes.md)
