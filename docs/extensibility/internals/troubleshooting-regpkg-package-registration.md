---
title: RegPkg 包注册疑难解答 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- RegPkg
ms.assetid: f33f822f-697a-4bad-9c10-554b4c8f6246
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 386a1a17c036207d122e4b3c7cb142a628dcfe38
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72722274"
---
# <a name="troubleshooting-regpkg-package-registration"></a>RegPkg 包注册疑难解答
> [!NOTE]
> 在 Visual Studio 中注册包的首选方法是使用 .pkgdef 文件。 这允许扩展部署，而无需访问系统注册表。 .Pkgdef 文件是使用[CreatePkgDef 实用程序](../../extensibility/internals/createpkgdef-utility.md)创建的。

 若要在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中使用 RegPkg 注册包，你必须使用适用于你的包的 RegPkg 版本。

## <a name="regpkg-versions-related-to-package-versions"></a>与包版本相关的 RegPkg 版本
 RegPkg 有两个版本。 @No__t_0 中包含一个版本。 使用此版本注册使用以下程序集之一生成的包：

1. VisualStudioShell。

2. VisualStudioShell .dll

3. VisualStudioShell。

   它无法注册使用以前的 VisualStudio 程序集生成的包。

   更早版本的 RegPkg 可以注册使用 VisualStudio 程序集生成的包。 但是，它无法注册使用该程序集的更高版本生成的包。

## <a name="see-also"></a>请参阅
- [VSPackage](../../extensibility/internals/vspackages.md)