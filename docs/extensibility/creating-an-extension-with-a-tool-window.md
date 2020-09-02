---
title: 使用工具窗口创建扩展 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
ms.assetid: 585b0a3a-f85b-4f92-81bb-9ca499bb8a89
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 597b84854dd398abee9dc21090e085273bc94c75
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85903892"
---
# <a name="create-an-extension-with-a-tool-window"></a>使用工具窗口创建扩展

在此过程中，您将了解如何使用 VSIX 项目模板和 **自定义工具窗口** 项模板来创建具有工具窗口的扩展。

## <a name="prerequisites"></a>先决条件

 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

### <a name="create-a-tool-window"></a>创建工具窗口

1. 创建名为 **FirstWindow**的 VSIX 项目。 可以通过搜索 "vsix" 在 " **新建项目** " 对话框中找到 VSIX 项目模板。

2. 项目打开时，添加一个名为 **MyWindow**的工具窗口项模板。 在**解决方案资源管理器**中，右键单击项目节点，然后选择 "**添加**  >  **新项**"。 在 "**添加新项**" 对话框中，切换到 " **Visual c #**  >  **扩展性**" 并选择 "**自定义工具窗口**"。 在窗口底部的 " **名称** " 字段中，将工具窗口文件的名称更改为 *MyWindow.cs*。

3. 生成项目并启动调试。

   此时将显示 Visual Studio 的实验实例。 有关实验实例的详细信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。

4. 在实验实例中，请参阅**查看**  >  **其他窗口**。

   应该会看到 **MyWindow**的菜单项。 请单击此按钮。

   应会看到带有标题 **MyWindow** 的工具窗口，并显示 " **单击我！" 按钮。**
