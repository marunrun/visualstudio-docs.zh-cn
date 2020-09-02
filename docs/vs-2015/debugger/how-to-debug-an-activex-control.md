---
title: 如何：调试 ActiveX 控件 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vc.controls.debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- testing [Visual Studio], test containers
- ActiveX control container debugging [Visual Studio]
- debugging ActiveX controls
- data-bound controls, ActiveX
- test container
- containers, specifying for debug sessions
- ActiveX controls, debugging
- testing [Visual Studio], ActiveX controls
ms.assetid: bbc02cf7-a7e6-44fe-99af-87a43e1d7251
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9524ab08ab955609f29f437e8a1576af02738aa1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704455"
---
# <a name="how-to-debug-an-activex-control"></a>如何：调试 ActiveX 控件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

备注
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在“工具”菜单上选择“导入和导出设置”。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
 若要调试 ActiveX 控件，必须指定一个容器（可执行文件）用于运行控件。  
  
### <a name="to-specify-a-container-for-the-debug-session"></a>为调试会话指定容器  
  
1. 在“解决方案资源管理器”中，选择项目。  
  
2. 从“视图”菜单中选择“属性页” 。  
  
3. 在“项目属性页”对话框中，打开“配置属性”文件夹并选定“调试”  。  
  
4. 在“调试”类别下，找到“命令”属性 。  
  
5. 指定容器的路径名。 例如，C:\Program Files\Internet Explorer\IEXPLORE.EXE。  
  
6. 如果指定 Internet Explorer 作为容器，并且正在使用 Active Desktop，请在“命令自变量”框中键入 `/new`。  
  
7. 单击 **“确定”** 。  
  
     如果在“项目属性页”对话框中没有指定容器，则可在开始调试时指定容器。 选择执行命令开始调试时，将出现[调试会话的可执行文件](../debugger/executable-for-debugging-session-dialog-box.md)对话框。 在对话框中指定容器的路径名。  
  
## <a name="see-also"></a>另请参阅  
 [ActiveX 控件](https://msdn.microsoft.com/library/52aaec4d-3889-402e-b57d-758078f8ac57)   
 [用测试容器测试属性和事件](https://msdn.microsoft.com/library/626867cf-fe53-4c30-8973-55bb93ef3917)   
 [COM 和 ActiveX 调试](../debugger/com-and-activex-debugging.md)   
 [在 Visual Studio 中进行调试](../debugger/debugging-in-visual-studio.md)
