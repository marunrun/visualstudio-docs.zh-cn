---
title: 注册和注销 Vspackage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: e25e7a46-6a55-4726-8def-ca316f553d6b
caps.latest.revision: 36
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1f6bc85fb00c15831dcf1a9f64e4b886272df218
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193822"
---
# <a name="registering-and-unregistering-vspackages"></a>注册和注销 VSPackage
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

特性用于注册 VSPackage，但  
  
## <a name="registering-a-vspackage"></a>注册 VSPackage  
 属性可用于控制托管的 Vspackage 的注册。 .Pkgdef 文件中包含所有的注册信息。 基于文件的注册的详细信息，请参阅[CreatePkgDef 实用工具](../extensibility/internals/createpkgdef-utility.md)。  
  
 下面的代码演示如何使用标准注册特性注册你的 VSPackage。  
  
```csharp  
[PackageRegistration(UseManagedResourcesOnly = true)]  
[Guid("0B81D86C-0A85-4f30-9B26-DD2616447F95")]  
public sealed class BasicPackage : Package  
{. . .}  
```  
  
## <a name="unregistering-an-extension"></a>注销扩展  
 如果你已尝试过很多不同的 Vspackage 使用，并想要从实验实例中删除它们，可以只需运行**重置**命令。 寻找**重置 Visual Studio 实验实例**在主页上的计算机，或从命令行运行以下命令：  
  
```vb  
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe" /Reset /VSInstance=14.0 /RootSuffix=Exp  
```  
  
 如果你想要卸载已在您的 Visual Studio 的开发实例安装的扩展，请转到**工具 / 扩展和更新**，找到扩展，然后单击**卸载**。  
  
 如果出于某种原因这两个方法成功如何卸载该扩展，则可按如下所示注销 VSPackage 程序集从命令行：  
  
```  
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\regpkg” /unregister <pathToVSPackage assembly>  
```  
  
## <a name="see-also"></a>请参阅  
 [VSPackage](../extensibility/internals/vspackages.md)
