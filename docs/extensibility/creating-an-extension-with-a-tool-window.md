---
title: 使用工具窗口创建扩展 |微软文档
ms.date: 3/16/2019
ms.topic: conceptual
ms.assetid: 585b0a3a-f85b-4f92-81bb-9ca499bb8a89
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 17f72cf130c5ff0f2d6d03ca8c460aa98ea39111
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739540"
---
# <a name="create-an-extension-with-a-tool-window"></a>使用工具窗口创建扩展

在此过程中，您将了解如何使用 VSIX 项目模板和**自定义工具窗口**项模板使用工具窗口创建扩展。

## <a name="prerequisites"></a>先决条件

 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

### <a name="create-a-tool-window"></a>创建工具窗口

1. 创建名为**FirstWindow 的**VSIX 项目。 您可以通过搜索"vsix"在 **"新项目**"对话框中找到 VSIX 项目模板。

2. 打开项目时，添加名为**MyWindow**的工具窗口项模板。 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 在 **"添加新项目"** 对话框中，转到**可视化 C#** > **可扩展性**并选择 **"自定义工具窗口**"。 在窗口底部的 **"名称"** 字段中，将工具窗口文件名更改为*MyWindow.cs*。

3. 生成项目并启动调试。

   视觉工作室的实验实例出现。 有关实验实例的详细信息，请参阅[实验实例](../extensibility/the-experimental-instance.md)。

4. 在实验例中，转到**查看** > **其他 Windows**。

   您应该会看到 **"我的窗口"** 的菜单项。 请单击此按钮。

   您应该会看到一个工具窗口，标题为 **"我的窗口"，** 并显示一个按钮，上面写着 **"单击我！"**
