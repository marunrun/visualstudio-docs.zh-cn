---
title: 如何：向 VSIX 包添加依赖项 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- package reference
- package assembly
- package dll
- vsix reference
ms.assetid: 8f20177b-dab9-43a3-b959-81a591b451d6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 063767f8f50793253c236db5d5b90e1d6db1bff4
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905864"
---
# <a name="how-to-add-a-dependency-to-a-vsix-package"></a>如何：向 VSIX 包添加依赖项

你可以设置一个 VSIX 包部署，用于安装目标计算机上尚不存在的任何依赖项。 若要实现此目的，请将 VSIX 依赖项包含到*source.extension.vsixmanifest*文件。

## <a name="to-add-a-dependency"></a>添加依赖项

1. 在 "**设计**" 视图中打开*source.extension.vsixmanifest*文件。 单击 "**依赖项**" 选项卡，然后单击 "**新建**"。

2. 添加已安装的扩展：在 "**添加新的依赖项**" 对话框中，选择 "**已安装的扩展**"，然后对于 "**名称**"，请在列表中选择一个扩展。

3. 添加另一个未安装的 VSIX：在 "**添加新依赖项**" 对话框中，选择 "文件**系统上的文件**"，然后使用 "**浏览**" 按钮选择该 vsix。

## <a name="require-a-specific-visual-studio-release"></a>需要特定的 Visual Studio 版本

例如，如果你的扩展需要 Visual Studio 2017 的特定版本，则它依赖于在15.3 中发布的功能，你可以在 VSIX **InstallationTarget**中指定内部版本号。 例如，版本15.3 的生成号为 "15.0.26730.3"。 可在[此处](../install/visual-studio-build-numbers-and-release-dates.md)查看生成编号的版本映射。 请注意，使用版本号 "15.3" 将不能正常工作。

如果扩展需要15.3 或更高版本，则需要将**InstallationTarget 版本**声明为 [15.0.26730.3，16.0）：

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```

VSIXInstaller 将检测早期版本的 Visual Studio，并通知用户需要进行更高版本的更新。

## <a name="see-also"></a>另请参阅

- [VSIX 扩展架构1.0 引用](https://msdn.microsoft.com/library/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)
- [VSIX 包的解析](../extensibility/anatomy-of-a-vsix-package.md)
- [为 Windows Installer 部署准备扩展](../extensibility/preparing-extensions-for-windows-installer-deployment.md)
