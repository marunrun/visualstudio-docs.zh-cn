---
title: 如何：更新 Visual Studio 扩展 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- update package
- update extension
- new package version
ms.assetid: 93f79774-7b79-4dd6-94ad-13698f72c257
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 237a1139a7a314cf99b5edbd8993abefe04592c8
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66324874"
---
# <a name="how-to-update-a-visual-studio-extension"></a>如何：更新 Visual Studio 扩展
可以通过使用你的系统上更新 Visual Studio 扩展**扩展和更新**若要安装的更新的版本。 如果您创建扩展的更新的版本，您可以将其表示为更新的 VSIX 清单中的版本号递增。

 安装更新时传入的扩展的 VSIX 清单具有相同`ID`已安装的证书和更高版本作为`Version`数。 如果`Version`数是相同或更低时，无法安装此包。 如果`ID`值不匹配、 尚未安装的包识别为单独的扩展。

 若要帮助防止冲突，在开发过程中，我们建议您卸载早期版本的扩展正在运行，并还卸载或禁用发生潜在冲突的任何其他扩展。

## <a name="to-update-an-extension-on-your-system"></a>若要更新你的系统上的扩展

1. 在  “工具”菜单上，单击  “扩展和更新”。

2. 在左窗格中，单击**更新**。

3. 在中间窗格中，单击你想要安装的更新。

     更新扩展的版本号显示在右窗格中，以及其他信息。

4. 在右窗格的底部，单击**更新**。

## <a name="to-publish-an-update-of-an-extension"></a>若要发布扩展的更新

1. 在 Visual Studio 中，打开你想要更新的扩展的解决方案。 进行更改。

    > [!IMPORTANT]
    > 无符号不会自动更新所有用户扩展。 你始终应登录你的扩展。

2. 在中**解决方案资源管理器**，打开*source.extension.manifest*。

3. 在清单设计器中的数字将值增加**版本**字段。

4. 保存解决方案，并生成它。

5. 上传新 *.vsix*文件 (在 * \bin\Debug\*项目文件夹中的) 到[Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) Web 站点。

     当具有扩展的早期版本的用户身份打开**扩展和更新**，新版本将出现在**更新**列表中，前提是该工具将自动查找更新。

     可以启用或禁用自动检查更新的底部**更新**窗格 (**可用更新的启用/禁用自动检测**)，哪些更改**检查更新**中设置**工具** > **选项** > **环境** >  **扩展和更新**。

    > [!NOTE]
    > 从 Visual Studio 2015 Update 2 开始，你可以指定 (在**工具** > **选项** > **环境** >  **扩展和更新**) 是否需要自动更新为每用户扩展、 所有用户扩展或两者 （默认设置）。

## <a name="see-also"></a>请参阅
- [VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)
- [查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)