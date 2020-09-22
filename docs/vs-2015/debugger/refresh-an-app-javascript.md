---
title: " (JavaScript) 中刷新应用 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- JavaScript debugging, refreshing pages [Windows Store apps]
- debugging, refreshing pages [Windows Store apps]
- DOM Explorer, Refresh [Windows Store apps]
- Refresh [Windows Store apps]
ms.assetid: fd99ee60-fa94-46df-8b17-369f60bfd908
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b5b8be97212f4510002a78e6565fc9884930db89
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840574"
---
# <a name="refresh-an-app-javascript"></a>刷新应用程序 (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

适用于 Windows 和 Windows Phone] (。将 windows_and_phone_content.png "windows_and_phone_content" )   
  
 你可以在调试时对代码进行更改，然后通过选择 "**调试**" 工具栏上的 "**刷新 Windows 应用程序**" 按钮，使用 JavaScript 刷新应用商店应用。 选择此按钮将重新加载应用程序，但不会停止并重新启动调试器。 通过“刷新”功能，可修改 HTML、CSS 和 JavaScript 代码并迅速看到结果。 Windows 应用商店和 Windows Phone 应用商店应用均支持此功能。  
  
 刷新功能不保持应用程序状态，也不反映对应用程序的以下更改：  
  
- 程序包清单文件更改，其中包括对程序包清单中指定图像的更改。  
  
- 引用更改（如添加或移除 SDK 引用）或 Windows 运行时组件（.winmd 文件）更改。  
  
- 资源更改，如对 .resjson 文件中字符串的更改。  
  
- 导致路径名更改、新建项目文件或删除文件的项目文件更改。  
  
- 项目和项属性更改（如对所选调试设备的更改）或对文件的程序包操作的更改（在“属性”窗口中）。  
  
> [!IMPORTANT]
> 在更改引用或包清单或者进行上面的列表中指定的其他更改时，必须停止并重新启动调试器以更新 HTML、CSS 和 JavaScript 源文件。  
  
### <a name="to-refresh-an-app"></a>刷新应用程序  
  
1. 在 Visual Studio 中，使用“导航应用”项目模板创建一个新项目。  
  
     它可以是 Windows 应用商店应用、Windows Phone 应用商店应用或通用应用。  
  
2. 在 Visual Studio 中打开模板后，选择一个调试目标。  
  
     如果 Windows Phone 项目是你的当前启动项目，请将 Windows Phone 仿真程序选为调试目标。 否则，请选择 " **模拟器** " 或 " **本地计算机**"。  
  
     ![选择调试目标列表](../debugger/media/js-select-target.png "JS_Select_Target")  
  
3. 按 F5 以在调试模式下运行应用程序。  
  
4. 切换到 Visual Studio。 （按 F12。）  
  
5. 在**解决方案资源管理器**的**页面**  >  **主**文件夹中，打开 home.html。  
  
6. 将页标题文本从  
  
    ```html  
    Welcome to yourAppName!  
    ```  
  
     改为类似如下所示的内容：  
  
    ```html  
    Hello!  
    ```  
  
7. 单击“刷新 Windows 应用”按钮，该按钮如下所示：![“刷新 Windows 应用”按钮](../debugger/media/js-refresh.png "JS_Refresh")。 （或按 F4。）  
  
8. 切换到该应用程序。 将重新加载该应用程序，但不重新启动调试器，并显示新的页面标题。  
  
## <a name="see-also"></a>另请参阅  
 [快速入门：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md)
