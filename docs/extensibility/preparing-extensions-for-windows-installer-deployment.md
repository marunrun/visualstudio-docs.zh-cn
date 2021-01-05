---
title: 准备 Windows Installer 部署的扩展 |Microsoft Docs
description: 了解如何准备一个项目，该项目的默认输出是一个要包含在安装项目中的 VSIX 包。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- vsix msi
ms.assetid: 5ee2d1ba-478a-4cb7-898f-c3b4b2ee834e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ba494af91d3d40720493b27e7381660ece3fba69
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97862905"
---
# <a name="prepare-extensions-for-windows-installer-deployment"></a>为 Windows Installer 部署准备扩展
不能使用 Windows Installer 包 (MSI) 来部署 VSIX 包。 不过，您可以提取用于 MSI 部署的 VSIX 包的内容。 本文档演示如何准备一个项目，该项目的默认输出是一个要包含在安装项目中的 VSIX 包。

## <a name="prepare-an-extension-project-for-windows-installer-deployment"></a>为 Windows Installer 部署准备扩展项目
 在添加到安装项目之前，请在新的扩展项目中执行这些步骤。

### <a name="to-prepare-an-extension-project-for-windows-installer-deployment"></a>为 Windows Installer 部署准备扩展项目

1. 创建包含 VSIX 清单的 VSPackage、MEF 组件、编辑器修饰或其他扩展性项目类型。

2. 在代码编辑器中打开 VSIX 清单。

3. 将 `InstalledByMsi` VSIX 清单的元素设置为 `true` 。 有关 VSIX 清单的详细信息，请参阅 [vsix 扩展架构2.0 引用](../extensibility/vsix-extension-schema-2-0-reference.md)。

     这会阻止 VSIX 安装程序尝试安装该组件。

4. 右键单击 " **解决方案资源管理器** 中的项目，然后单击" **属性**"。

5. 选择 " **VSIX** " 选项卡。

6. 选中标签 " **将 VSIX 内容复制到以下位置** " 框，然后键入安装项目将选取文件的路径。

## <a name="extract-files-from-an-existing-vsix-package"></a>从现有 VSIX 包提取文件
 如果没有源文件，请执行以下步骤将现有 VSIX 包的内容添加到安装项目。

### <a name="to-extract-files-from-an-existing-vsix-package"></a>从现有 VSIX 包提取文件

1. 重命名 *。* 包含要 *filename.zip**的文件扩展名* 的 vsix 文件。

2. 将 *.zip* 文件的内容复制到目录中。

3. 从目录中删除 *[Content_types] .xml* 文件。

4. 如前面的过程所示，编辑 VSIX 清单。

5. 将剩余文件添加到安装项目。

## <a name="see-also"></a>另请参阅
- [Visual Studio 安装程序部署](/previous-versions/2kt85ked(v=vs.120))
- [演练：创建自定义操作](/previous-versions/visualstudio/visual-studio-2010/d9k65z2d(v=vs.100))