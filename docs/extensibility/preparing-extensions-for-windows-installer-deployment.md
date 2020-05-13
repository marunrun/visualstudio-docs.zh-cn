---
title: 为 Windows 安装程序部署准备扩展 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- vsix msi
ms.assetid: 5ee2d1ba-478a-4cb7-898f-c3b4b2ee834e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8636dfbbad06192e5edbb61a9a784f64b8f3f14f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702028"
---
# <a name="prepare-extensions-for-windows-installer-deployment"></a>为 Windows 安装程序部署准备扩展
不能使用 Windows 安装程序包 （MSI） 部署 VSIX 包。 但是，您可以提取用于 MSI 部署的 VSIX 包的内容。 本文档演示如何准备默认输出为 VSIX 包的项目，以便包含在安装程序项目中。

## <a name="prepare-an-extension-project-for-windows-installer-deployment"></a>为 Windows 安装程序部署准备扩展项目
 在添加到安装程序项目之前，对新的扩展项目执行这些步骤。

### <a name="to-prepare-an-extension-project-for-windows-installer-deployment"></a>为 Windows 安装程序部署准备扩展项目

1. 创建 VSPackage、MEF 组件、编辑器修饰或其他包含 VSIX 清单的扩展性项目类型。

2. 打开代码编辑器中的 VSIX 清单。

3. 将`InstalledByMsi`VSIX 清单的元素设置为`true`。 有关 VSIX 清单的详细信息，请参阅[VSIX 扩展架构 2.0 引用](../extensibility/vsix-extension-schema-2-0-reference.md)。

     这可以防止 VSIX 安装程序尝试安装组件。

4. 右键单击**解决方案资源管理器**中的项目，然后单击 **"属性**"。

5. 选择**VSIX**选项卡。

6. 选中标记为将**VSIX 内容复制到以下位置**的框，然后键入安装程序项目将拾取文件的路径。

## <a name="extract-files-from-an-existing-vsix-package"></a>从现有 VSIX 包中提取文件
 执行这些步骤，在没有源文件时，将现有 VSIX 包的内容添加到安装程序项目中。

### <a name="to-extract-files-from-an-existing-vsix-package"></a>从现有 VSIX 包中提取文件

1. 重命名 *。包含*从*文件名.vsix*到*filename.zip*的扩展名的 VSIX 文件。

2. 将 *.zip*文件的内容复制到目录中。

3. 从目录中删除 *[Content_types]xml*文件。

4. 编辑 VSIX 清单，如上一过程所示。

5. 将其余文件添加到安装程序项目中。

## <a name="see-also"></a>请参阅
- [可视化工作室安装程序部署](https://msdn.microsoft.com/library/121be21b-b916-43e2-8f10-8b080516d2a0)
- [演练：创建自定义操作](/previous-versions/visualstudio/visual-studio-2010/d9k65z2d(v=vs.100))
