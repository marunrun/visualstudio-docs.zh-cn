---
title: RegPkg 实用工具 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- regpkg, registration utility
- registration, regpkg utility
ms.assetid: 1683ee18-59d1-4bab-a674-dd00dd960de3
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e5b4e6384730492e0f34470bbe4676ce0d9012c3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310976"
---
# <a name="regpkg-utility"></a>RegPkg 实用工具
> [!NOTE]
> 在 Visual Studio 中注册包的首选的方法是通过使用.pkgdef 文件。 这样可以扩展部署而无需访问是必需的 VSIX 部署的系统注册表。 通过使用创建 Pkgdef 文件[CreatePkgDef 实用工具](../../extensibility/internals/createpkgdef-utility.md)。 Visual Studio 包部署的详细信息，请参阅[传送 Visual Studio 扩展](../../extensibility/shipping-visual-studio-extensions.md)。

 RegPkg.exe 实用程序注册与 VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使其准备好部署。 此实用程序在后台使用 VSPackage 开发过程。 它作为生成过程的一部分运行，以便可以生成并在实验性配置单元中运行 VSPackage。

 RegPkg 可以用多种格式生成系统注册表脚本。 您可以将这些脚本在部署项目，例如.msi 项目或 Windows Installer XML 工具集文件中。

 RegPkg.exe 是通常位于\< *Visual Studio SDK 安装路径*> \VisualStudioIntegration\Tools\Bin\RegPkg.exe。 RegPkg 使用以下语法：

```
RegPkg [/root:<root>] [/regfile:<regfile>] [/rgsfile:<rgsfile> [/rgm]] [/vrgfile:<vrgfile>] [/codebase | /assembly] [/unregister] AssemblyPath
```

 在指定 /root:root 执行注册

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 根。

 /regfile:FileName 创建.reg 文件而不更新注册表。  不能用于 /vrgfile 或 /rgsfile 或 /wixfile。

 /rgsfile:FileName 创建 rgs 文件而不更新注册表。  不能用于 /vrgfile 或 /regfile 或 /wixfile。

 /vrgfile:FileName 创建.vrg 文件而不更新注册表。  不能用于 /regfile 或 /rgsfile 或 /wixfile。

 /rgm 创建.rgm 文件除了 rgs 文件。  必须与 /rgsfile 结合。

 /wixfile:FileName 创建与 Windows Installer XML 工具集兼容的文件而不更新注册表。  不能用于 /regfile 或 /rgsfile 或 /vrgfile。

 / 基本代码强制注册到的基本代码而不是程序集。

 /assembly 强制注册程序集，而不是个基本代码。

 / 注销 Unregisters 此包。  不能使用

 与 /regfile 或 /vrgfile 或 /rgsfile 或 /wixfile。

## <a name="see-also"></a>请参阅
- [VSPackage](../../extensibility/internals/vspackages.md)
- [对 RegPkg 包注册进行故障排除](../../extensibility/internals/troubleshooting-regpkg-package-registration.md)