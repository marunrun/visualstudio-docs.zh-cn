---
title: 选择 VSPackage 的安装目录 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, installation directory
ms.assetid: 01fbbb5b-f747-446c-afe0-2a081626a945
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ead19e9f50201ab795e3c3f68b661037d309d98d
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90011900"
---
# <a name="choose-the-installation-directory-for-a-vspackage"></a>选择 VSPackage 的安装目录
VSPackage 及其支持文件必须位于用户的文件系统上。 位置取决于 VSPackage 是托管的还是非托管的、并排版本控制方案和用户选择。

## <a name="unmanaged-vspackages"></a>非托管 Vspackage
 非托管 VSPackage 是可以安装在任何位置的 COM 服务器。 其注册信息必须准确反映其位置。 安装程序用户界面 (UI) 应提供 Windows Installer 属性值的子目录的默认位置 `ProgramFilesFolder` 。 例如：

*&lt;ProgramFilesFolder &gt; \\ &lt; MyCompany &gt; \\ &lt; MyVSPackageProduct &gt; \V1。0\\*

 应该允许用户更改默认目录，以适应保留小型启动分区并更喜欢在另一卷上安装应用程序和工具的用户。

 如果并排方案使用了版本控制的 VSPackage，则可以使用子目录来存储不同的版本。 例如：

 *&lt;ProgramFilesFolder &gt; \\ &lt; MyCompany &gt; \\ &lt; MyVSPackageProduct v1.0 &gt; \\ \\ 2002\\*

 *&lt;ProgramFilesFolder &gt; \\ &lt; MyCompany &gt; \\ &lt; MyVSPackageProduct v1.0 &gt; \\ \\ 2003\\*

 *&lt;ProgramFilesFolder &gt; \\ &lt; MyCompany &gt; \\ &lt; MyVSPackageProduct v1.0 &gt; \\ \\ 2005\\*

## <a name="managed-vspackages"></a>托管的 VSPackage
 托管的 Vspackage 也可以安装在任何位置。 但是，你应考虑始终将它们安装到全局程序集缓存 (GAC) 以减少程序集加载时间。 由于托管 Vspackage 始终具有强名称的程序集，因此在 GAC 中安装它们意味着其强名称签名验证仅在安装时才需要。 在文件系统中的其他位置安装的强名称程序集必须在每次加载时验证其签名。 在 GAC 中安装托管 Vspackage 时，请使用 regpkg 工具的 **/assembly** 开关来写入指向程序集的强名称的注册表项。

 如果将托管的 Vspackage 安装在 GAC 以外的位置，请遵循为非托管 Vspackage 提供的更早建议，以选择目录层次结构。 使用 regpkg 工具的 **/codebase** 开关写入指向 VSPackage 程序集路径的注册表项。

 有关详细信息，请参阅 [注册和注销 vspackage](../../extensibility/registering-and-unregistering-vspackages.md)。

## <a name="satellite-dlls"></a>附属 DLL
 按照约定，VSPackage 附属 Dll （其中包含特定区域设置的资源）位于 *VSPackage* 目录的子目录中。 子目录对应于区域设置 ID (LCID) 值。

 " [管理 vspackage](../../extensibility/managing-vspackages.md) " 一文指示注册表项控制 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 实际查找 VSPACKAGE 的附属 DLL 的位置。 不过， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 尝试按照以下顺序在名为 LCID 值的子目录中加载附属 DLL：

1. Visual Studio LCID (默认 LCID;例如，对于英语) 为*\ 1033*

2. 默认的子语言为默认的 LCID。

3. 系统默认的 LCID。

4. 默认语言为系统默认的 LCID。

5. 美国英语 (*\ 1033* 或 *.\0x409*) 。

如果 VSPackage DLL 包含资源，并且 **SatelliteDll\DllName** 注册表项指向它，则 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 会尝试按上述顺序加载它们。

## <a name="see-also"></a>请参阅
- [在共享和版本控制之间进行选择 Vspackage](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [管理 VSPackage](../../extensibility/managing-vspackages.md)
- [管理包注册](/previous-versions/bb166783(v=vs.100))