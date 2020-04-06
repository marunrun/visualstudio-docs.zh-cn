---
title: 注册单个文件生成器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, custom tools
- custom tools, defining registry settings
ms.assetid: db7592c0-1273-4843-9617-6e2ddabb6ca8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1cea2ebba4739695393447a36e9842ade1670954
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705813"
---
# <a name="registering-single-file-generators"></a>注册单个文件生成器
要使自定义工具在 中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]可用，必须注册它，以便[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]实例化它并将其与特定的项目类型关联。

### <a name="to-register-a-custom-tool"></a>注册自定义工具

1. 在HKEY_CLASSES_ROOT的情况下，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]在本地注册表或系统注册表中注册自定义工具 DLL。

    例如，下面是托管 MSDataSetGenerator 自定义工具的注册信息，该工具附带[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]：

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\CLSID\{E76D53CC-3D4F-40A2-BD4D-4F3419755476}]
   @="COM+ class: Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"
   "InprocServer32"="C:\\WINDOWS\\system32\\mscoree.dll"
   "ThreadingModel"="Both"
   "Class"="Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"
   "Assembly"="Microsoft.VSDesigner, Version=14.0.0.0, Culture=Neutral, PublicKeyToken=b03f5f7f11d50a3a"
   ```

2. 在\\生成器*GUID*下[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]所需的配置单元中创建注册表项，其中*GUID*是由特定语言的项目系统或服务定义的 GUID。 密钥的名称将成为自定义工具的编程名称。 自定义工具键具有以下值：

   - （默认值）

        可选。 提供自定义工具的用户友好说明。 此参数是可选的，但建议使用。

   - CLSID

        必需。 指定实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>的 COM 组件的类库的标识符。

   - 生成设计时间来源

        必需。 指示此自定义工具生成的文件中的类型是否可供可视化设计器使用。 对于视觉设计器不可用的类型，此参数的值需要为 （零） 0，对于可视化设计器可用的类型，则需要 （1） 1。

   > [!NOTE]
   > 您必须为希望自定义工具可用的每种语言分别注册自定义工具。

    例如，MSDataSet生成器为每个语言注册一次：

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{164b10b9-b200-11d0-8c61-00a0c91e29d5}\MSDataSetGenerator]
   @="Microsoft VB Code Generator for XSD"
   "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"
   "GeneratesDesignTimeSource"=dword:00000001

   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{fae04ec1-301f-11d3-bf4b-00c04f79efbc}\MSDataSetGenerator]
   @="Microsoft C# Code Generator for XSD"
   "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"
   "GeneratesDesignTimeSource"=dword:00000001
   ```

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>
- [实现单个文件生成器](../../extensibility/internals/implementing-single-file-generators.md)
- [向可视化设计器公开类型](../../extensibility/internals/exposing-types-to-visual-designers.md)
- [BuildManager 对象介绍](https://msdn.microsoft.com/library/50080ec2-c1c9-412c-98ef-18d7f895e7fa)
