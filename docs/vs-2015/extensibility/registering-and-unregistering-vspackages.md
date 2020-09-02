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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193822"
---
# <a name="registering-and-unregistering-vspackages"></a>注册和注销 VSPackage
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用特性来注册 VSPackage，但  
  
## <a name="registering-a-vspackage"></a>注册 VSPackage  
 您可以使用属性来控制托管 Vspackage 的注册。 所有注册信息都包含在一个 .pkgdef 文件中。 有关基于文件的注册的详细信息，请参阅 [CreatePkgDef Utility](../extensibility/internals/createpkgdef-utility.md)。  
  
 下面的代码演示如何使用标准注册特性来注册你的 VSPackage。  
  
```csharp  
[PackageRegistration(UseManagedResourcesOnly = true)]  
[Guid("0B81D86C-0A85-4f30-9B26-DD2616447F95")]  
public sealed class BasicPackage : Package  
{. . .}  
```  
  
## <a name="unregistering-an-extension"></a>注销扩展  
 如果你已经尝试过大量不同的 Vspackage，并想要将它们从实验实例中删除，则可以直接运行 **Reset** 命令。 在计算机的 "开始" 页上查找 **"重置 Visual Studio 实验实例** "，或从命令行运行以下命令：  
  
```vb  
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe" /Reset /VSInstance=14.0 /RootSuffix=Exp  
```  
  
 如果要卸载已安装在 Visual Studio 开发实例上的扩展，请依次单击 " **工具"/"扩展和更新**" 和 " **卸载**"。  
  
 如果出于某种原因，这两种方法都不会在卸载扩展时成功完成，您可以从命令行中注销 VSPackage 程序集，如下所示：  
  
```  
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\regpkg” /unregister <pathToVSPackage assembly>  
```  
  
## <a name="see-also"></a>另请参阅  
 [VSPackages](../extensibility/internals/vspackages.md)
