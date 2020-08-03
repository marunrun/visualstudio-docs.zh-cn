---
title: RegPkg 包注册疑难解答 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- RegPkg
ms.assetid: f33f822f-697a-4bad-9c10-554b4c8f6246
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b5266579ff235a0f6c4f3e555d79d5a00de2c194
ms.sourcegitcommit: 9a7fb8556a5f3dbb4459122fefc7e7a8dfda753a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87234856"
---
# <a name="troubleshooting-regpkg-package-registration"></a>RegPkg 包注册疑难解答
> [!NOTE]
> 在 Visual Studio 中注册包的首选方法是使用 .pkgdef 文件。 这允许扩展部署，而无需访问系统注册表。 .Pkgdef 文件是使用[CreatePkgDef 实用程序](../../extensibility/internals/createpkgdef-utility.md)创建的。

 若要在中使用 RegPkg 注册包 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，你必须使用适用于你的包的 RegPkg 版本。

## <a name="regpkg-versions-related-to-package-versions"></a>与包版本相关的 RegPkg 版本
 RegPkg 有两个版本。 其中包含一个版本 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 使用此版本注册使用以下程序集之一生成的包：

1. Microsoft.VisualStudioShell.9.0.dll

2. Microsoft.VisualStudioShell.10.0.dll

3. Microsoft.VisualStudioShell.11.0.dll

   它无法注册使用以前 Microsoft.VisualStudio.Shell.dll 的程序集生成的包。

   RegPkg 的早期版本可以注册使用 Microsoft.VisualStudio.Shell.dll 程序集生成的包。 但是，它无法注册使用该程序集的更高版本生成的包。

## <a name="see-also"></a>另请参阅
- [VSPackages](../../extensibility/internals/vspackages.md)
- [Visual Studio 故障排除](/troubleshoot/visualstudio/welcome-visual-studio/)
