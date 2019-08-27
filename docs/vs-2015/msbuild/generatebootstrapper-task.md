---
title: GenerateBootstrapper 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GenerateBootstrapper
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateBootstrapper task
- GenerateBootstrapper task [MSBuild]
ms.assetid: ca3ba2c6-d2ea-41f2-b7e3-0fc2b0730460
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 488caf02a20b4f0855df1ba2ef64c85e70e1a6a4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149628"
---
# <a name="generatebootstrapper-task"></a>GenerateBootstrapper 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

提供自动化方式来检测、下载和安装应用程序及其必备组件。 它可以作为集成不同的安装程序的单个安装程序为组成应用程序的所有组件提供服务。  
  
## <a name="task-parameters"></a>任务参数  
 下表描述了 `GenerateBootstrapper` 任务的参数。  
  
- `ApplicationFile`  
  
   可选 `String` 参数。  
  
   指定引导程序将用于在安装所有系统必备组件后开始安装此应用程序的文件。 如果 `BootstrapperItems` 和 `ApplicationFile` 均未指定参数，将产生生成错误。  
  
- `ApplicationName`  
  
   可选 `String` 参数。  
  
   指定引导程序将安装的应用程序的名称。 此名称将显示在引导程序在安装过程中使用的 UI 中。  
  
- `ApplicationRequiresElevation`  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则安装在目标计算机上时，组件使用提升的权限运行。  
  
- `ApplicationUrl`  
  
   可选 `String` 参数。  
  
   指定承载应用程序安装程序的 Web 位置。  
  
- `BootstrapperComponentFiles`  
  
   可选 `String[]` 输出参数。  
  
   指定引导程序包文件的生成位置。  
  
- `BootstrapperItems`  
  
   可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。  
  
   指定要置入引导程序中的产品。 传递给此参数的项应具有以下语法：  
  
  ```  
  <BootstrapperItem  
      Include="ProductCode">  
      <ProductName>  
          ProductName  
      </ProductName>  
  </BootstrapperItem>  
  ```  
  
   `Include` 属性用来表示应安装的必备组件的名称。 `ProductName` 项元数据是可选的，并且在找不到包的情况下，生成引擎将其用作用户友好名称。 这些项不是必需的 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 输入参数，除非没有指定任何 `ApplicationFile`。 对于必须为你的应用程序安装的每个必备组件，应包括一个项。  
  
   如果 `BootstrapperItems` 和 `ApplicationFile` 均未指定参数，将产生生成错误。  
  
- `BootstrapperKeyFile`  
  
   可选 `String` 输出参数。  
  
   指定 setup.exe 的生成位置  
  
- `ComponentsLocation`  
  
   可选 `String` 参数。  
  
   指定一个位置，以供引导程序查找要安装的安装必备组件。 此参数可以具有下列值：  
  
  - `HomeSite`：指示必备组件正由组件供应商托管。  
  
  - `Relative`：指示必备组件位于应用程序的同一位置。  
  
  - `Absolute`：指示所有组件都可在集中式 URL 处找到。 此值应与 `ComponentsUrl` 输入参数结合使用。  
  
    如果未指定 `ComponentsLocation`，则默认情况下使用 `HomeSite`。  
  
- `ComponentsUrl`  
  
   可选 `String` 参数。  
  
   指定包含安装必备组件的 URL。  
  
- `CopyComponents`  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则引导程序将所有输出文件都复制到 `OutputPath` 参数中指定的路径。 `BootstrapperComponentFiles` 参数的值应全部位于该路径中。 如果为 `false`，将不会复制这些文件，且 `BootstrapperComponentFiles` 值基于 `Path` 参数的值。  此参数的默认值为 `true`。  
  
- `Culture`  
  
   可选 `String` 参数。  
  
   指定用于引导程序 UI 和安装必备组件的区域性。 如果指定的区域性不可用，则该任务使用 `FallbackCulture` 参数的值。  
  
- `FallbackCulture`  
  
   可选 `String` 参数。  
  
   指定用于引导程序 UI 和安装必备组件的辅助区域性。  
  
- `OutputPath`  
  
   可选 `String` 参数。  
  
   指定用于复制 setup.exe 和所有包文件的位置。  
  
- `Path`  
  
   可选 `String` 参数。  
  
   指定所有可用的系统必备包的位置。  
  
- `SupportUrl`  
  
   可选 `String` 参数。  
  
   指定要在引导程序安装失败时提供的 URL  
  
- `Validate`  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则引导程序对指定输入的引导程序项执行 XSD 验证。 此参数的默认值为 `false`。  
  
## <a name="remarks"></a>备注  
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)。  
  
## <a name="example"></a>示例  
 以下示例使用 `GenerateBootstrapper` 任务来安装将 [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] 作为必备组件安装的应用程序。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <BootstrapperFile Include="Microsoft.Net.Framework.2.0">  
            <ProductName>Microsoft .NET Framework 2.0</ProductName>  
        </BootstrapperFile>  
    </ItemGroup>  
  
    <Target Name="BuildBootstrapper">  
        <GenerateBootstrapper  
            ApplicationFile="WindowsApplication1.application"  
            ApplicationName="WindowsApplication1"  
            ApplicationUrl="http://mycomputer"  
            BootstrapperItems="@(BootstrapperFile)"  
            OutputPath="C:\output" />  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>请参阅  
 [任务](../msbuild/msbuild-tasks.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)
