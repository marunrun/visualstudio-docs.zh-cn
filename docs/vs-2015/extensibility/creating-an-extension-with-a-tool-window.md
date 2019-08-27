---
title: 使用工具窗口创建扩展 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 585b0a3a-f85b-4f92-81bb-9ca499bb8a89
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 94c8335b8d723ef20c04cfffe6b3788d71ecaa4f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62431844"
---
# <a name="creating-an-extension-with-a-tool-window"></a>使用工具窗口创建扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在此过程中，了解如何使用 VSIX 项目模板并**自定义工具窗口**要使用的工具窗口创建扩展项模板。  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
### <a name="creating-a-tool-window"></a>创建工具窗口  
  
1. 创建一个名为的 VSIX 项目**FirstWindow**。 可以查找中的 VSIX 项目模板**新的项目**下的对话框**Visual C# / 可扩展性**。  
  
2. 项目打开后，添加一个名为的工具窗口项模板**FirstWindow**。 在中**解决方案资源管理器**，右键单击项目节点并选择**添加 / 新项**。 在中**添加新项**对话框中，转到**Visual C# / 可扩展性**，然后选择**自定义工具窗口**。 在中**名称**在窗口底部字段中，将工具窗口文件名称更改为**FirstWindow.cs**。  
  
3. 生成项目并启动调试。  
  
     将显示 Visual Studio 的实验实例。 有关实验实例的详细信息，请参阅[实验实例](../extensibility/the-experimental-instance.md)。  
  
4. 在实验实例中，转到**视图 / 其他 Windows**。  
  
     你应看到的菜单项**FirstWindow**。 单击它。  
  
     应看到一个带有标题的工具窗口**FirstWindow**和按钮 saying**单击我 ！。**
