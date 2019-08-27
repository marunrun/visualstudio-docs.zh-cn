---
title: 为 VSPackage 选择安装目录 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, installation directory
ms.assetid: 01fbbb5b-f747-446c-afe0-2a081626a945
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 249efe70cdcc2cf8ef600ca4d9e009e094e1b105
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309112"
---
# <a name="choose-the-installation-directory-for-a-vspackage"></a>为 VSPackage 选择安装目录
VSPackage 和及其支持文件必须位于用户的文件系统上。 位置取决于 VSPackage 是否托管或非托管，通过并行版本控制方案和用户的选择。

## <a name="unmanaged-vspackages"></a>非托管的 Vspackage
 非托管的 VSPackage 是可以在任何位置中安装的 COM 服务器。 其注册信息必须准确地反映其位置。 在安装程序用户界面 (UI) 应提供的默认位置为的子目录`ProgramFilesFolder`Windows Installer 属性值。 例如：

*&lt;ProgramFilesFolder&gt;\\&lt;MyCompany&gt;\\&lt;MyVSPackageProduct&gt;\V1.0\\*

 应允许用户更改以适应保持小的引导分区的用户的默认目录，并想要在另一个卷上安装应用程序和工具。

 如果通过并行方案使用版本控制的 VSPackage，你可以使用子目录来存储不同版本。 例如：

 *&lt;ProgramFilesFolder&gt;\\&lt;MyCompany&gt;\\&lt;MyVSPackageProduct&gt;\\V1.0\\2002\\*

 *&lt;ProgramFilesFolder&gt;\\&lt;MyCompany&gt;\\&lt;MyVSPackageProduct&gt;\\V1.0\\2003\\*

 *&lt;ProgramFilesFolder&gt;\\&lt;MyCompany&gt;\\&lt;MyVSPackageProduct&gt;\\V1.0\\2005\\*

## <a name="managed-vspackages"></a>托管的 VSPackage
 也可以在任何位置安装托管的 Vspackage。 但是，应考虑始终将它们安装到全局程序集缓存 (GAC) 来减少程序集加载时间。 托管的 Vspackage 始终是强名称的程序集，因为它们安装在 GAC 中意味着仅在安装时，采用其强名称签名验证。 文件系统中的其他位置安装了强名称的程序集必须具有每次加载时验证其签名。 当用户在 GAC 中安装托管的 Vspackage 时，使用 regpkg 工具 **/assembly**开关来写入注册表项指向程序集的强名称。

 如果在 GAC 之外的某个位置中安装托管的 Vspackage，请按照早期的非托管的 Vspackage 提供的选择目录层次结构的建议。 使用 regpkg 工具 **/codebase**开关来写入注册表项指向 VSPackage 程序集的路径。

 有关详细信息，请参阅[注册和注销 Vspackage](../../extensibility/registering-and-unregistering-vspackages.md)。

## <a name="satellite-dlls"></a>附属 Dll
 按照约定，VSPackage 附属 Dll，包含对特定区域设置的资源，位于中的子目录*VSPackage*目录。 子目录对应于区域设置 ID (LCID) 值。

 [管理 Vspackage](../../extensibility/managing-vspackages.md)一文指明的注册表项控制在何处[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]实际上对为 VSPackage 的外观的附属资源 DLL。 但是，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]尝试加载附属 DLL 的 LCID 值，按以下顺序命名的子目录中：

1. 默认 LCID (Visual Studio LCID; 例如， *\1033*英语)

2. 使用默认子语言的默认 LCID。

3. 系统默认 LCID。

4. 使用默认子语言的系统默认 LCID。

5. 美国英语 ( *。 \1033*或 *。 \0x409*)。

如果 VSPackage DLL 包含资源和**SatelliteDll\DllName**注册表项指向了它，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]尝试按上述顺序加载它们。

## <a name="see-also"></a>请参阅
- [共享和版本控制的 Vspackage 之间进行选择](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [管理 VSPackages](../../extensibility/managing-vspackages.md)
- [管理包注册](https://msdn.microsoft.com/library/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)