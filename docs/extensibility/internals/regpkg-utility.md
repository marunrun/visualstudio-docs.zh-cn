---
title: RegPkg 实用程序 |Microsoft Docs
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
ms.openlocfilehash: f811eb37da730d63e199a0e378b8a9122143649e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72724451"
---
# <a name="regpkg-utility"></a>RegPkg 实用工具
> [!NOTE]
> 在 Visual Studio 中注册包的首选方法是使用 .pkgdef 文件。 这样就可以实现扩展部署，而无需访问系统注册表，这是对 VSIX 部署的要求。 .Pkgdef 文件是使用[CreatePkgDef 实用程序](../../extensibility/internals/createpkgdef-utility.md)创建的。 有关 Visual Studio 包部署的详细信息，请参阅[发布 Visual Studio 扩展](../../extensibility/shipping-visual-studio-extensions.md)。

 RegPkg 实用程序将一个 VSPackage 注册到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 并为部署做好准备。 此实用程序在 VSPackage 开发期间在幕后使用。 它作为生成过程的一部分运行，以便您可以在实验性 hive 中生成并运行 VSPackage。

 RegPkg 可以采用多种格式生成系统注册表脚本。 可以将这些脚本合并到部署项目（如 .msi 项目）或 Windows Installer XML 工具集文件中。

 RegPkg 通常位于 \<*Visual STUDIO SDK 安装路径*> \VisualStudioIntegration\Tools\Bin\RegPkg.exe。 RegPkg 遵循以下语法：

```
RegPkg [/root:<root>] [/regfile:<regfile>] [/rgsfile:<rgsfile> [/rgm]] [/vrgfile:<vrgfile>] [/codebase | /assembly] [/unregister] AssemblyPath
```

 /root： root 在指定的下执行注册

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 根。

 /regfile： FileName 创建一个 .reg 文件，而不是更新注册表。  不能与/vrgfile 或/rgsfile 或/wixfile. 一起使用。

 /rgsfile： FileName 创建一个 .rgs 文件，而不是更新注册表。  不能与/vrgfile 或/regfile 或/wixfile. 一起使用。

 /vrgfile： FileName 创建 vrg 文件，而不是更新注册表。  不能与/regfile 或/rgsfile 或/wixfile. 一起使用。

 /rgm 除了 rgs 文件外，还会创建一个 rgm-f4-ycn 文件。  必须与/rgsfile. 结合

 /wixfile： FileName 创建 Windows Installer 的与 XML 工具集兼容的文件，而不是更新注册表。  不能与/regfile 或/rgsfile 或/vrgfile. 一起使用。

 /codebase 强制注册 CodeBase 而不是程序集。

 /assembly 强制注册程序集而不是基本代码。

 /unregister 注销此包。  不能使用

 with/regfile、/vrgfile 或/rgsfile 或/wixfile。

## <a name="see-also"></a>请参阅
- [VSPackage](../../extensibility/internals/vspackages.md)
- [对 RegPkg 包注册进行故障排除](../../extensibility/internals/troubleshooting-regpkg-package-registration.md)