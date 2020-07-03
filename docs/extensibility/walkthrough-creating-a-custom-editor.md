---
title: 演练：创建自定义编辑器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - create
ms.assetid: d090abb6-d99f-4083-a3db-cd16bf81ce7d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4713931d70fd91dd57b85bc6fc749e62e03eb20b
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905915"
---
# <a name="walkthrough-create-a-custom-editor"></a>演练：创建自定义编辑器
VSPackage 项目模板可使用 c + + 创建一个简单的自定义编辑器。 VSPackage 项目模板不再支持 c # 或 Visual Basic 项目。 有关详细信息，请参阅[Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。

## <a name="prerequisites"></a>必备条件
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="the-visual-studio-package-project-template"></a>Visual Studio 包项目模板
 可以在 " **c + + 扩展性**" 文件夹下的 "**新建项目**" 对话框中找到 Visual Studio 包项目模板。

### <a name="to-create-a-vspackage-using-the-visual-studio-package-template"></a>使用 Visual Studio 包模板创建 VSPackage

1. 使用 Visual Studio 包模板创建项目。

2. 选择 "**自定义编辑器**" 选项，然后单击 "**下一步**"。 此时将显示**编辑器选项**页。

3. 在编辑器的 "**名称**" 框中，键入编辑器的名称。 在 "**文件扩展名**" 框中，键入要与编辑器关联的文件扩展名。 编辑器可用于具有此扩展名的文件。 文件扩展名仅为 Visual Studio 注册，不适用于 Windows。 在 "**默认**文件名" 框中键入用编辑器创建的新文档的默认文件名。

4. 单击“完成” **** 以在指定的文件夹中创建 VSPackage。

### <a name="to-test-your-custom-editor"></a>测试自定义编辑器

1. 在 "**文件**" 菜单上，指向 "**新建**"，然后单击 "**文件**"。

2. 在 "**新建文件**" 对话框的 "**已安装的模板**" 窗格中，选择文件模板，然后选择您注册的文件类型。

3. 单击 "**打开**" 以查看和编辑该文档。

     编辑器支持剪切和粘贴、查找和替换以及打开和加载操作。

## <a name="see-also"></a>另请参阅
- [VSPackage](../extensibility/internals/vspackages.md)
