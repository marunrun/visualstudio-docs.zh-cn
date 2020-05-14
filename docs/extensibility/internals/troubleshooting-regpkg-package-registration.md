---
title: 故障排除 RegPkg 包装注册 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- RegPkg
ms.assetid: f33f822f-697a-4bad-9c10-554b4c8f6246
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ebae9f7c5b4d1a6dcfee20c3b36c02f8ead2e0bc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704333"
---
# <a name="troubleshooting-regpkg-package-registration"></a>RegPkg 包注册疑难解答
> [!NOTE]
> 在 Visual Studio 中注册包的首选方法是使用 .pkgdef 文件。 这允许扩展部署，而无需访问系统注册表。 Pkgdef 文件是通过使用[CreatePkgDef 实用程序](../../extensibility/internals/createpkgdef-utility.md)创建的。

 要在 中使用 RegPkg 注册[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]包，必须使用适合您的包的 RegPkg 版本。

## <a name="regpkg-versions-related-to-package-versions"></a>与包版本相关的 RegPkg 版本
 RegPkg 有两个版本。 中包括一个版本[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 使用此版本可以注册使用以下程序集之一生成的包：

1. 微软.VisualStudioShell.9.0.dll

2. 微软.VisualStudioShell.10.0.dll

3. 微软.VisualStudioShell.11.0.dll

   它不能注册使用早期的 Microsoft.VisualStudio.Shell.dll 程序集构建的包。

   早期版本的 RegPkg 可以注册使用 Microsoft.VisualStudio.shell.dll 程序集构建的包。 但是，它不能注册使用该程序集的更高版本生成的包。

## <a name="see-also"></a>请参阅
- [VSPackage](../../extensibility/internals/vspackages.md)
