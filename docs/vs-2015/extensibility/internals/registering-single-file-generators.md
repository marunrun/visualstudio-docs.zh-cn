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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696107"
---
# <a name="registering-single-file-generators"></a>注册单个文件生成器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

若要使自定义工具中可用[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，因此必须注册该[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]可以实例化并将其关联与特定项目类型。  
  
### <a name="to-register-a-custom-tool"></a>若要注册的自定义工具  
  
1. 或者注册自定义工具 DLL 中[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]本地注册表或在系统注册表中，在 HKEY_CLASSES_ROOT 下。  
  
     例如，下面是托管的 MSDataSetGenerator 自定义工具，它附带的注册信息[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]:  
  
    ```  
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\CLSID\{E76D53CC-3D4F-40A2-BD4D-4F3419755476}]  
    @="COM+ class: Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"  
    "InprocServer32"="C:\\WINDOWS\\system32\\mscoree.dll"  
    "ThreadingModel"="Both"  
    "Class"="Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"  
    "Assembly"="Microsoft.VSDesigner, Version=14.0.0.0, Culture=Neutral, PublicKeyToken=b03f5f7f11d50a3a"  
    ```  
  
2. 创建注册表项中的所需[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]hive 下生成器\\*GUID*其中*GUID*由特定语言的项目系统或服务定义 GUID。 密钥的名称将成为您的自定义工具的编程名称。 自定义工具密钥具有以下值：  
  
    - (默认)  
  
         可选。 提供自定义工具的用户友好说明。 此参数是可选的但建议这样做。  
  
    - CLSID  
  
         必需。 指定实现的 COM 组件的类库的标识符<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>。  
  
    - GeneratesDesignTimeSource  
  
         必需。 指示是否通过此自定义工具生成的文件中的类型将提供给可视化设计器。 此参数的值必须是类型向可视化设计器不可用 （零） 0 或类型可用于可视化设计器 （一个） 1。  
  
    > [!NOTE]
    > 必须注册为其所需的自定义工具，可用于每种语言单独的自定义工具。  
  
     例如，MSDataSetGenerator 自行注册一次为每种语言：  
  
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
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>   
 [实现单个文件生成器](../../extensibility/internals/implementing-single-file-generators.md)   
 [确定项目的默认 Namespace](../../misc/determining-the-default-namespace-of-a-project.md)   
 [公开到可视化设计器的类型](../../extensibility/internals/exposing-types-to-visual-designers.md)   
 [BuildManager 对象介绍](https://msdn.microsoft.com/50080ec2-c1c9-412c-98ef-18d7f895e7fa)
