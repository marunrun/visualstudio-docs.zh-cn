---
title: RegPkg 包注册进行故障排除 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: troubleshooting
helpviewer_keywords:
- RegPkg
ms.assetid: f33f822f-697a-4bad-9c10-554b4c8f6246
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 241975e475252a18d5e5a91c6e8c4fb40c067a95
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63441192"
---
# <a name="troubleshooting-regpkg-package-registration"></a>RegPkg 包注册疑难解答
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!NOTE]
> 在 Visual Studio 中注册包的首选的方法是通过使用.pkgdef 文件。 这样可以扩展部署而无需访问系统注册表。 通过使用创建 Pkgdef 文件[CreatePkgDef 实用工具](../../extensibility/internals/createpkgdef-utility.md)。  
  
 若要使用 RegPkg 中的注册包[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，必须使用适合于您的包的 RegPkg 的版本。  
  
## <a name="regpkg-versions-related-to-package-versions"></a>与包版本相关的 RegPkg 版本  
 有两个版本的 RegPkg。 一个版本包含在[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 使用此版本已通过以下程序集生成的包注册：  
  
1. Microsoft.VisualStudioShell.9.0.dll  
  
2. Microsoft.VisualStudioShell.10.0.dll  
  
3. Microsoft.VisualStudioShell.11.0.dll  
  
   它不能注册已使用早期 Microsoft.VisualStudio.Shell.dll 程序集生成的包。  
  
   在早期版本的 RegPkg 可以注册使用 Microsoft.VisualStudio.Shell.dll 程序集生成的包。 但是，它不能使用该程序集的更高版本生成的包进行注册。  
  
## <a name="see-also"></a>请参阅  
 [发布产品](../../misc/releasing-a-visual-studio-integration-product.md)
