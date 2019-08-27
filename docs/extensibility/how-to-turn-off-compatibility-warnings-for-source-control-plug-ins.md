---
title: 关闭源代码管理插件的兼容性警告 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, turning off compatibility warnings
- compatibility warnings, turning off
ms.assetid: ba318e12-921b-4b7a-a8c2-12c712be1dbf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6dc8edcb6ee10be8b020424d8f8c247770a98f27
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66324811"
---
# <a name="how-to-turn-off-compatibility-warnings-for-source-control-plug-ins"></a>如何：关闭的源代码管理插件的兼容性警告
使用源代码管理中的时，用户可能会看到几个兼容性警告[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 显示警告取决于源代码管理插件的功能，可禁用详细信息如下。

### <a name="to-disable-the-warning-to-ensure-optimal-source-control-integration-with-visual-studio"></a>若要禁用此警告："以确保获得最佳的源代码管理与 Visual Studio 集成"

- 设置以下注册表项 （如有必要，将添加值）：

   **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\DontDisplayCheckDotNETCompatible = dword: 00000001**

   此警告将显示所有非[!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)]插件。

### <a name="to-disable-the-warning-the-installed-source-control-provider-does-not-support-all-the-capabilities"></a>若要禁用此警告："已安装的源代码管理提供程序不支持所有功能"

- 设置以下两个注册表值 （如有必要，将添加值）：

     **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\WarnedOldMSSCCIProvider = dword:00000000**

    **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\UseOldSCC = dword:00000001**

     如果源代码管理插件不显式支持可重入性的多个项目 （即，如果它可以一次检查中只有一个文件和项目），将显示此警告。

     最好是支持可重入性 (`SCC_CAP_REENTRANT`功能); 这样做将消除此警告。 但是，如果这种支持不能，可以设置这些注册表项。

## <a name="see-also"></a>请参阅
- [功能标志](../extensibility/capability-flags.md)