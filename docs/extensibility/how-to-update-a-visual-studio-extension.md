---
title: 如何：更新视觉工作室扩展 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- update package
- update extension
- new package version
ms.assetid: 93f79774-7b79-4dd6-94ad-13698f72c257
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 266c0a49db1bca03cec0eb68301445102173df3d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710657"
---
# <a name="how-to-update-a-visual-studio-extension"></a>如何：更新可视化工作室扩展
您可以使用**扩展和更新**来安装更新的版本，从而更新系统上的 Visual Studio 扩展。 如果创建扩展的更新版本，则可以通过在 VSIX 清单中增加版本号来将其表示为更新版本。

 当传入扩展的 VSIX 清单与已安装的一个`ID`数字和更高的`Version`数字相同时，将安装更新。 如果`Version`数字相同或更低，则无法安装包。 如果`ID`这些值不匹配，则尚未安装的包将识别为单独的扩展。

 为了帮助防止开发过程中的冲突，我们建议您卸载正在进行的扩展的早期版本，并卸载或禁用任何其他可能冲突的扩展。

## <a name="to-update-an-extension-on-your-system"></a>更新系统上的扩展

1. 在 **** “工具”菜单上，单击 ****“扩展和更新”。

2. 在左侧窗格中，单击"**更新**"。

3. 在中间窗格中，单击要安装的更新。

     更新的扩展的版本号与其他信息一起显示在右侧窗格中。

4. 在右侧窗格的底部，单击"**更新**"。

## <a name="to-publish-an-update-of-an-extension"></a>发布扩展的更新

1. 在 Visual Studio 中，打开要更新的扩展的解决方案。 进行更改。

    > [!IMPORTANT]
    > 未签名的所有用户扩展不会自动更新。 应始终在扩展中签名。

2. 在**解决方案资源管理器**中，*开源.扩展.清单*。

3. 在清单设计器中，增加 **"版本"** 字段中的数字值。

4. 保存解决方案并构建它。

5. 将新的 *.vsix*文件（在项目的 _bin_\*调试文件夹中）上载到[可视化工作室应用商店](https://marketplace.visualstudio.com/vs)网站。

     当具有早期版本的扩展的用户打开**扩展和更新**时，新版本将显示在 **"更新**"列表中，前提是该工具设置为自动查找更新。

     您可以在 **"更新"** 窗格（**启用/禁用自动检测可用更新**）中启用或禁用自动检查更新，这将更改 **"工具** > **选项** > **环境** > **扩展和更新**"中的 **"检查更新**"设置。

    > [!NOTE]
    > 从 Visual Studio 2015 更新 2 开始，您可以指定（在**工具** > **选项** > **环境** > **扩展和更新**中），是否要自动更新每个用户扩展、所有用户扩展或两者（默认设置）。

## <a name="see-also"></a>请参阅
- [VSIX 软件包的剖析](../extensibility/anatomy-of-a-vsix-package.md)
- [查找和使用可视化工作室扩展](../ide/finding-and-using-visual-studio-extensions.md)
