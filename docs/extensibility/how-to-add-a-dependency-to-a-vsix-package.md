---
title: 如何：将依赖项添加到 VSIX 包 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- package reference
- package assembly
- package dll
- vsix reference
ms.assetid: 8f20177b-dab9-43a3-b959-81a591b451d6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ee6ebeb776e6aa85d5fba200ac357a7375fa2b99
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341051"
---
# <a name="how-to-add-a-dependency-to-a-vsix-package"></a>如何：将依赖项添加到 VSIX 包

您可以设置安装尚不存在于目标计算机上的任何依赖项的 VSIX 包部署。 若要实现此目的，包括到 VSIX 依赖项*source.extension.vsixmanifest*文件。

## <a name="to-add-a-dependency"></a>若要添加的依赖项

1. 打开*source.extension.vsixmanifest*中的文件**设计**视图。 转到**依赖项**选项卡，单击**新建**。

2. 若要添加的已安装的扩展： 在**添加新依赖关系**对话框中，选择**已安装扩展**，然后针对**名称**，选择列表中的扩展。

3. 若要添加另一个未安装的 VSIX： 中**添加新依赖关系**对话框中，选择**在文件系统上的文件**，然后使用**浏览**按钮以选择 VSIX。

## <a name="require-a-specific-visual-studio-release"></a>需要特定的 Visual Studio 版本

如果您的扩展插件需要特定版本的 Visual Studio 2017，例如，它依赖于版本 15.3 中一个功能，您可以在 VSIX 中指定的内部版本号**InstallationTarget**。 例如，版本 15.3 有"15.0.26730.3"内部版本号。 您所见发布生成号的映射[此处](../install/visual-studio-build-numbers-and-release-dates.md)。 请注意，使用发行版号"15.3"将无法正常运行。

如果您的扩展插件需要 15.3 或更高版本，则需要声明**InstallationTarget 版本**作为 [15.0.26730.3, 16.0):

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```

Vsixinstaller 找将检测 Visual Studio 的早期版本，并通知用户，则需要更高版本的更新。

## <a name="see-also"></a>请参阅

- [VSIX 扩展架构 1.0 参考](https://msdn.microsoft.com/library/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)
- [VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)
- [准备 Windows 安装程序部署扩展](../extensibility/preparing-extensions-for-windows-installer-deployment.md)
