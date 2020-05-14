---
title: 关闭源控制插件的兼容性警告 |微软文档
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
ms.openlocfilehash: 22dd3821426aa1dae6265c520ddac60dd93e1c5e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710729"
---
# <a name="how-to-turn-off-compatibility-warnings-for-source-control-plug-ins"></a>如何：关闭源代码管理插件的兼容性警告
在 中[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]使用源代码时，用户可能会看到多个兼容性警告。 显示的警告取决于源代码管理插件的功能，可以在此处禁用，如下所示。

### <a name="to-disable-the-warning-to-ensure-optimal-source-control-integration-with-visual-studio"></a>禁用警告："确保与 Visual Studio 的最佳源代码管理集成"

- 设置以下注册表项（如有必要，添加值）：

   **HKEY_CURRENT_USER_软件_微软_VisualStudio_8.0_源代码控制\不要显示检查DotNET兼容 = dword：00000001**

   将显示此警告，用于所有非[!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)]插件。

### <a name="to-disable-the-warning-the-installed-source-control-provider-does-not-support-all-the-capabilities"></a>禁用警告："已安装的源代码管理提供程序不支持所有功能"

- 设置以下两个注册表值（如有必要添加值）：

     **HKEY_CURRENT_USER_软件\微软_VisualStudio_8.0_源代码控制\警告OldMSSCCI提供商 = dword：0000000**

    **HKEY_CURRENT_USER_软件\微软_VisualStudio_8.0_源代码控制\使用OldSCC = dword：00000001**

     如果源代码管理插件不显式支持多个项目的重化（也就是说，如果一次只能签入一个文件和项目），则显示此警告。

     最好支持重化（`SCC_CAP_REENTRANT`能力）;这样做将删除此警告。 但是，如果无法进行此支持，则可以设置这些注册表项。

## <a name="see-also"></a>请参阅
- [功能标志](../extensibility/capability-flags.md)
