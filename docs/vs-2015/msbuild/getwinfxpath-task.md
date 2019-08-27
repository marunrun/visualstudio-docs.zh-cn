---
title: GetWinFXPath 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- getting the directory of the current .NET Framework runtime [WPF MSBuild]
- GetWinFXPath task [WPF MSBuild], parameters
- GetWinFXPath task [WPF MSBuild]
- obtaining the path to the current .NET Framework runtime [WPF MSBuild]
ms.assetid: b1dfb467-f3d3-47f3-83ef-af7b0e33a772
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: da32f0bfce9edf652e19df6b68bc51ed92624d80
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65699023"
---
# <a name="getwinfxpath-task"></a>GetWinFXPath 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:Microsoft.Build.Tasks.Windows.GetWinFXPath> 任务返回当前 [!INCLUDE[TLA#tla_winfx](../includes/tlasharptla-winfx-md.md)] 运行时的目录。  
  
## <a name="task-parameters"></a>任务参数  
  
|参数|说明|  
|---------------|-----------------|  
|`WinFXPath`|可选的 **String** 输出参数。<br /><br /> 指定 [!INCLUDE[TLA2#tla_winfx](../includes/tla2sharptla-winfx-md.md)] 运行时的实际路径。|  
|`WinFXNativePath`|必需的 **String** 参数。<br /><br /> 指定本机 [!INCLUDE[TLA2#tla_titlewinfx](../includes/tla2sharptla-titlewinfx-md.md)] 运行时的路径。|  
|`WinFXWowPath`|必需的 **String** 参数。<br /><br /> 指定 64 位系统上 32 位 **Windows on Windows** 模块中的 [!INCLUDE[TLA#tla_winfx](../includes/tlasharptla-winfx-md.md)] 程序集的路径。|  
  
## <a name="remarks"></a>备注  
 如果在 64 位处理器上执行 <xref:Microsoft.Build.Tasks.Windows.GetWinFXPath> 任务，则 WinFXPath 参数会设置为 WinFXWowPath 参数中存储的路径；否则，WinFXPath 参数会设置为 WinFXNativePath 参数中存储的路径。  
  
## <a name="example"></a>示例  
 如下示例演示了如何使用 **GetWinFXPath** 任务来检测 [!INCLUDE[TLA2#tla_titlewinfx](../includes/tla2sharptla-titlewinfx-md.md)] 运行时的本机路径。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask   
    TaskName="Microsoft.Build.Tasks.Windows.GetWinFXPath"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="GetWinFXPathTask">  
    <GetWinFXPath  
      WinFXNativePath="c:\WinFXNative"   
      WinFXWowPath="c:\WinFXWowNative" />  
  </Target>  
  <Import Project="$(MSBuildBinPath)\Microsoft.WinFX.targets" />  
</Project>  
```  
  
## <a name="see-also"></a>请参阅  
 [WPF MSBuild 引用](../msbuild/wpf-msbuild-reference.md)   
 [任务参考](../msbuild/wpf-msbuild-task-reference.md)   
 [MSBuild 参考](../msbuild/msbuild-reference.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)   
 [Building a WPF Application (WPF)](https://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)（生成 WPF 应用程序 (WPF)）
