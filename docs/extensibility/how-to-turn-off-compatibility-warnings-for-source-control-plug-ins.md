---
title: 关闭源代码管理插件的警告
description: 在 Visual Studio 中使用源代码管理时，用户可能会看到几个兼容性警告。 了解如何禁用这些警告。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, turning off compatibility warnings
- compatibility warnings, turning off
ms.assetid: ba318e12-921b-4b7a-a8c2-12c712be1dbf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f5607f4a92a14b692f20d509e014991d461815bd
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96993544"
---
# <a name="how-to-turn-off-compatibility-warnings-for-source-control-plug-ins"></a>如何：关闭源代码管理插件的兼容性警告

在中使用源代码管理时，用户可能会看到几个兼容性警告 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 显示的警告取决于源代码管理插件的功能，可在此处详细说明。

### <a name="to-disable-the-warning-to-ensure-optimal-source-control-integration-with-visual-studio"></a>若要禁用警告： "确保与 Visual Studio 的最佳源代码管理集成"

- 如有必要，请设置以下注册表项 (添加值) ：

   **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\DontDisplayCheckDotNETCompatible = dword：00000001**

   对于所有非插件，都会显示此警告 [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] 。

### <a name="to-disable-the-warning-the-installed-source-control-provider-does-not-support-all-the-capabilities"></a>若要禁用警告： "安装的源代码管理提供程序不支持所有功能"

- 设置以下两个注册表值 (如有必要) 添加值：

     **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\WarnedOldMSSCCIProvider = dword：00000000**

    **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\UseOldSCC = dword：00000001**

     如果源代码管理插件不显式支持多个项目的重入， (即，如果每次只能签入一个文件和项目) ，则会显示此警告。

     最好 (功能) 支持重入 `SCC_CAP_REENTRANT` ; 这样做会消除此警告。 但是，如果无法进行此支持，则可以设置这些注册表项。

## <a name="see-also"></a>另请参阅

- [功能标志](../extensibility/capability-flags.md)
