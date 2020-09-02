---
title: 注册单个文件生成器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- registration, custom tools
- custom tools, defining registry settings
ms.assetid: db7592c0-1273-4843-9617-6e2ddabb6ca8
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6afcd708ac50a46ceb3359f0d2c0821e3b788f47
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696107"
---
# <a name="registering-single-file-generators"></a>注册单个文件生成器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

若要在中提供自定义工具 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，你必须注册它，以便可以对其进行 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 实例化并将其与特定的项目类型关联。  
  
### <a name="to-register-a-custom-tool"></a>注册自定义工具  
  
1. 在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 本地注册表或系统注册表中，在 "HKEY_CLASSES_ROOT" 下注册自定义工具 DLL。  
  
     例如，下面是托管 MSDataSetGenerator 自定义工具的注册信息，其中包含 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ：  
  
    ```  
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\CLSID\{E76D53CC-3D4F-40A2-BD4D-4F3419755476}]  
    @="COM+ class: Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"  
    "InprocServer32"="C:\\WINDOWS\\system32\\mscoree.dll"  
    "ThreadingModel"="Both"  
    "Class"="Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"  
    "Assembly"="Microsoft.VSDesigner, Version=14.0.0.0, Culture=Neutral, PublicKeyToken=b03f5f7f11d50a3a"  
    ```  
  
2. 在生成器 guid 下的所需配置单元中创建注册表项 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] \\ *GUID* ，其中*guid*是特定语言的项目系统或服务定义的 guid。 密钥名称将成为自定义工具的编程名称。 自定义工具键具有以下值：  
  
    - （默认值）  
  
         可选。 提供自定义工具的用户友好说明。 此参数是可选的，但建议使用。  
  
    - CLSID  
  
         必需。 指定实现的 COM 组件的类库的标识符 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 。  
  
    - GeneratesDesignTimeSource  
  
         必需。 指示此自定义工具所生成的文件中的类型是否可供可视化设计器使用。 对于可视化设计器不可用的类型，此参数的值需要 (零) 0; 对于可用于可视化设计器的类型，则需要 (一) 1。  
  
    > [!NOTE]
    > 您必须为您要为其提供自定义工具的每种语言分别注册自定义工具。  
  
     例如，MSDataSetGenerator 为每种语言注册一次自身：  
  
    ```  
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{164b10b9-b200-11d0-8c61-00a0c91e29d5}\MSDataSetGenerator]  
    @="Microsoft VB Code Generator for XSD"  
    "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"  
    "GeneratesDesignTimeSource"=dword:00000001  
  
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{fae04ec1-301f-11d3-bf4b-00c04f79efbc}\MSDataSetGenerator]  
    @="Microsoft C# Code Generator for XSD"  
    "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"  
    "GeneratesDesignTimeSource"=dword:00000001  
  
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{e6fdf8b0-f3d1-11d4-8576-0002a516ece8}\MSDataSetGenerator]  
    @="Microsoft J# Code Generator for XSD"  
    "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"  
    "GeneratesDesignTimeSource"=dword:00000001  
    ```  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>   
 [实现单文件生成器](../../extensibility/internals/implementing-single-file-generators.md)   
 [确定项目的默认命名空间](../../misc/determining-the-default-namespace-of-a-project.md)   
 [向可视化设计器公开类型](../../extensibility/internals/exposing-types-to-visual-designers.md)   
 [BuildManager 对象介绍](https://msdn.microsoft.com/50080ec2-c1c9-412c-98ef-18d7f895e7fa)
