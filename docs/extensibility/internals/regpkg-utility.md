---
title: RegPkg 实用程序 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- regpkg, registration utility
- registration, regpkg utility
ms.assetid: 1683ee18-59d1-4bab-a674-dd00dd960de3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cebfd7a9782a2760eb33f7e56bfe16b126fc6251
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705641"
---
# <a name="regpkg-utility"></a>RegPkg 实用工具
> [!NOTE]
> 在 Visual Studio 中注册包的首选方法是使用 .pkgdef 文件。 这允许扩展部署，而无需访问系统注册表，这是 VSIX 部署的要求。 Pkgdef 文件是通过使用[CreatePkgDef 实用程序](../../extensibility/internals/createpkgdef-utility.md)创建的。 有关可视化工作室包部署的详细信息，请参阅[传送视觉工作室扩展](../../extensibility/shipping-visual-studio-extensions.md)。

 RegPkg.exe 实用程序注册 VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]并为其进行部署。 此实用程序在 VSPackage 开发期间在后台使用。 它作为生成过程的一部分运行，以便您可以在实验配置单元中生成和运行 VSPackage。

 RegPkg 可以生成多种格式的系统注册表脚本。 您可以将这些脚本合并到部署项目中，如 .msi 项目或 Windows 安装程序 XML 工具集文件。

 RegPkg.exe 通常位于\<*视觉工作室 SDK 安装路径*>_VisualStudio 集成\工具\Bin_RegPkg.exe。 RegPkg 遵循以下语法：

```
RegPkg [/root:<root>] [/regfile:<regfile>] [/rgsfile:<rgsfile> [/rgm]] [/vrgfile:<vrgfile>] [/codebase | /assembly] [/unregister] AssemblyPath
```

 /root：根在指定下执行注册

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 根。

 /regfile：Filename 创建一个 .reg 文件，而不是更新注册表。  不能与 /vrgfile 或 /rgsfile 或 /wixfile 一起使用。

 /rgsfile：Filename 创建一个 .rgs 文件，而不是更新注册表。  不能与 /vrgfile 或 /regfile 或 /wixfile 一起使用。

 /vrgfile：Filename 创建一个 .vrg 文件，而不是更新注册表。  不能与 /regfile 或 /rgsfile 或 /wixfile 一起使用。

 /rgm 除了 rgs 文件之外，还创建一个 .rgm 文件。  必须与 /rgsfile 组合。

 /wixfile：文件名创建一个 Windows 安装程序 XML 工具集兼容文件，而不是更新注册表。  不能与 /regfile 或 /rgsfile 或 /vrgfile 一起使用。

 /代码库 强制注册代码库，而不是程序集。

 /程序集强制注册程序集，而不是代码库。

 /取消注册取消注册此包。  无法使用

 带 /regfile 或 /vrgfile 或 /rgsfile 或 /wixfile。

## <a name="see-also"></a>请参阅
- [VSPackage](../../extensibility/internals/vspackages.md)
- [对 RegPkg 包注册进行故障排除](../../extensibility/internals/troubleshooting-regpkg-package-registration.md)
