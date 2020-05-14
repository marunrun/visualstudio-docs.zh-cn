---
title: 为 VS 包选择安装目录 |微软文档
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
ms.openlocfilehash: b8391cbdd3a857ea4ebaf3a36655520935f1a128
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709763"
---
# <a name="choose-the-installation-directory-for-a-vspackage"></a>选择 VSPackage 的安装目录
VSPackage 及其支持文件必须位于用户的文件系统上。 位置取决于 VSPackage 是托管还是非托管、并行版本控制方案和用户选择。

## <a name="unmanaged-vspackages"></a>非托管 VS 包
 非托管 VSPackage 是可在任何位置安装的 COM 服务器。 其注册信息必须准确反映其位置。 安装程序用户界面 （UI） 应提供默认位置作为 Windows 安装程序属性值`ProgramFilesFolder`的子目录。 例如：

*&lt;程序文件文件夹&gt;\\&lt;我的公司&gt;\\&lt;MyVS包产品&gt;#V1.0\\*

 应允许用户更改默认目录，以适应保留小型引导分区并更愿意在另一卷上安装应用程序和工具的用户。

 如果并行方案使用版本化 VSPackage，则可以使用子目录来存储不同的版本。 例如：

 *&lt;程序文件文件夹&gt;\\&lt;我的公司&gt;\\&lt;MyVS&gt;\\包产品 V1.0\\2002\\*

 *&lt;程序文件文件夹&gt;\\&lt;我的公司&gt;\\&lt;MyVS&gt;\\包产品 V1.0\\2003\\*

 *&lt;程序文件文件夹&gt;\\&lt;我的公司&gt;\\&lt;MyVS&gt;\\包产品 V1.0\\2005\\*

## <a name="managed-vspackages"></a>托管的 VSPackage
 托管 VS 包也可以安装在任何位置。 但是，应考虑始终将它们安装到全局程序集缓存 （GAC） 以缩短程序集加载时间。 由于托管 VSPackages 始终是强名称程序集，因此在 GAC 中安装它们意味着其强名称签名验证仅在安装时才需要。 文件系统中其他位置安装的强命名程序集必须在每次加载时验证其签名。 在 GAC 中安装托管 VSPackages 时，请使用 regpkg 工具的 **/程序集**开关写入指向程序集的强名称的注册表项。

 如果在 GAC 以外的位置安装托管 VS 包，请按照前面为非托管 VSPackages 提供的建议来选择目录层次结构。 使用 regpkg 工具的 **/codebase**开关编写指向 VSPackage 程序集路径的注册表项。

 有关详细信息，请参阅[注册和取消注册 VS 包](../../extensibility/registering-and-unregistering-vspackages.md)。

## <a name="satellite-dlls"></a>附属 DLL
 按照惯例，包含特定区域设置资源的 VSPackage 卫星 DLL 位于*VSPackage*目录的子目录中。 子目录对应于区域设置 ID （LCID） 值。

 ["管理 VSPackages"](../../extensibility/managing-vspackages.md)一文指示注册表项[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]控制实际查找 VSPackage 的卫星 DLL 的位置。 但是，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]尝试按以下顺序在名为 LCID 值的子目录中加载卫星 DLL：

1. 默认 LCID（视觉工作室 LCID;例如，英语 *#1033）*

2. 默认 LCID 与默认子语言。

3. 系统默认 LCID。

4. 系统默认 LCID 与默认子语言。

5. 美国英语 *（.1033*或 *.\0x409*）。

如果您的 VSPackage DLL 包含资源，并且**SatelliteDll_DllName**注册表条目[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]指向它，则尝试按上述顺序加载它们。

## <a name="see-also"></a>请参阅
- [在共享和版本化 VS 包之间进行选择](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [管理 VSPackage](../../extensibility/managing-vspackages.md)
- [管理包注册](https://msdn.microsoft.com/library/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)
