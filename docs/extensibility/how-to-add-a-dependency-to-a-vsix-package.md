---
title: 如何：向 VSIX 包添加依赖项 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: f8b350f063c28762edf90edfe71330534451c75d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711069"
---
# <a name="how-to-add-a-dependency-to-a-vsix-package"></a>如何：向 VSIX 包添加依赖项

您可以设置 VSIX 包部署，该部署安装目标计算机上尚未存在的任何依赖项。 为此，请包括对*源.扩展.vsixmanifest*文件的 VSIX 依赖项。

## <a name="to-add-a-dependency"></a>添加依赖项

1. 在 **"设计"** 视图中打开*源.扩展.vsixmanifest*文件。 转到 **"依赖项"** 选项卡，然后单击 **"新建**"。

2. 要添加已安装的扩展：在 **"添加新依赖项"** 对话框中，选择 **"已安装扩展名**"，然后，对于 **"名称**"，请在列表中选择扩展名。

3. 要添加另一个未安装的 VSIX：在 **"添加新依赖项"** 对话框中，选择**文件系统上的"文件**"，然后使用 **"浏览"** 按钮选择 VSIX。

## <a name="require-a-specific-visual-studio-release"></a>需要特定的可视化工作室版本

例如，如果您的扩展需要 Visual Studio 2017 的特定版本，则它取决于 15.3 中发布的功能，则可以在 VSIX**安装目标**中指定内部版本号。 例如，版本 15.3 的生成号为"15.0.26730.3"。 你可以[在这里](../install/visual-studio-build-numbers-and-release-dates.md)看到版本映射以生成数字。 请注意，使用版本号"15.3"将不能正常工作。

如果您的扩展需要 15.3 或更高版本，您将声明**安装目标版本**为 [15.0.26730.3， 16.0）：

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```

VSIX安装程序将检测早期版本的 Visual Studio，并通知用户需要稍后的更新。

## <a name="see-also"></a>请参阅

- [VSIX 扩展架构 1.0 引用](https://msdn.microsoft.com/library/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)
- [VSIX 软件包的剖析](../extensibility/anatomy-of-a-vsix-package.md)
- [为 Windows 安装程序部署准备扩展](../extensibility/preparing-extensions-for-windows-installer-deployment.md)
