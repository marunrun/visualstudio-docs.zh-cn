---
title: 如何：关闭源代码管理插件的兼容性警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, turning off compatibility warnings
- compatibility warnings, turning off
ms.assetid: ba318e12-921b-4b7a-a8c2-12c712be1dbf
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a4397b2710a7de4addd97bfcbdb4f8e80e2b9c70
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204054"
---
# <a name="how-to-turn-off-compatibility-warnings-for-source-control-plug-ins"></a>如何：关闭源代码管理插件的兼容性警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在中使用源代码管理时，用户可能会看到几个兼容性警告 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 显示的警告取决于源代码管理插件的功能，可在此处详细说明。  
  
### <a name="to-disable-the-warning-to-ensure-optimal-source-control-integration-with-visual-studio"></a>若要禁用警告： "确保与 Visual Studio 的最佳源代码管理集成 ..."  
  
- 如有必要，请设置以下注册表项 (添加值) ：  
  
     HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl\DontDisplayCheckDotNETCompatible = dword：00000001  
  
     对于所有非插件，都会显示此警告 [!INCLUDE[vsvss](../includes/vsvss-md.md)] 。  
  
### <a name="to-disable-the-warning-the-installed-source-control-provider-does-not-support-all-the-capabilities"></a>若要禁用警告： "安装的源代码管理提供程序不支持所有功能 ..."  
  
- 设置以下两个注册表值 (如有必要) 添加值：  
  
     HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl\WarnedOldMSSCCIProvider = dword：00000000  
  
     HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl\UseOldSCC = dword：00000001  
  
     如果源代码管理插件不显式支持多个项目的重入， (即，如果每次只能签入一个文件和项目) ，则会显示此警告。  
  
     最好 (功能) 支持重入 `SCC_CAP_REENTRANT` ; 这样做会消除此警告。 但是，如果无法进行此支持，则可以设置这些注册表项。  
  
## <a name="see-also"></a>另请参阅  
 [功能标志](../extensibility/capability-flags.md)
