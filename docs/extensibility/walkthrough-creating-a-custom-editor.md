---
title: 演练：创建自定义编辑器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - create
ms.assetid: d090abb6-d99f-4083-a3db-cd16bf81ce7d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7eb376637fd72f3856415ee2527ec622fea02950
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697667"
---
# <a name="walkthrough-create-a-custom-editor"></a>演练：创建自定义编辑器
VSPackage 项目模板可以在C++中创建一个简单的自定义编辑器。 VSPackage 项目模板不再支持 C# 或可视化基本项目。 有关详细信息，请参阅[可视化工作室 SDK](../extensibility/visual-studio-sdk.md)。

## <a name="prerequisites"></a>先决条件
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="the-visual-studio-package-project-template"></a>可视化工作室包项目模板
 您可以在**C++"扩展性"** 文件夹下的"**新项目**"对话框中找到可视化工作室包项目模板。

### <a name="to-create-a-vspackage-using-the-visual-studio-package-template"></a>使用可视化工作室包模板创建 VS 包

1. 使用可视化工作室包模板创建项目。

2. 选择 **"自定义编辑器"** 选项，然后单击 **"下一步**"。 将显示 **"编辑器选项"** 页。

3. 在 **"编辑器名称"** 框中键入编辑器的名称。 在 **"文件扩展名"** 框中键入要与编辑器关联的文件扩展名。 您的编辑器可用于具有此扩展名的文件。 文件扩展名仅注册为 Visual Studio，而不是为 Windows 注册。 在 **"默认文件名"** 框中键入使用编辑器创建的新文档的默认文件名。

4. 单击“完成” **** 以在指定的文件夹中创建 VSPackage。

### <a name="to-test-your-custom-editor"></a>测试自定义编辑器

1. 在 **"文件"** 菜单上，指向 **"新建"，** 然后单击"**文件**"。

2. 在 **"新建文件**"对话框的"**已安装模板"** 窗格中，选择文件模板，然后选择您注册的文件类型。

3. 单击 **"打开"** 以查看和编辑文档。

     编辑器支持剪切和粘贴、查找和替换以及打开和关闭和加载操作。

## <a name="see-also"></a>请参阅
- [VSPackage](../extensibility/internals/vspackages.md)
