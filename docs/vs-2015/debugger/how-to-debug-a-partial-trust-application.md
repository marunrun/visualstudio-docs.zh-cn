---
title: 如何：调试部分信任应用程序 |Microsoft Docs
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
- debugging [Visual Studio], partial trust applications
- partial trust applications
- security [Visual Studio], partial trust applications
ms.assetid: 9d30ad92-28ce-4b21-91d8-698474cddf64
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 030fef750cc1e0f0932de32fca1a0ffef56bc8f3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704486"
---
# <a name="how-to-debug-a-partial-trust-application"></a>如何：调试部分信任应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

适用于 Windows 应用程序和控制台应用程序。  
  
 [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)轻松地部署部分信任应用程序，充分利用[代码访问安全性](https://msdn.microsoft.com/library/859af632-c80d-4736-8d6f-1e01b09ce127)来限制对计算机上的资源的访问。  
  
 部分信任的应用程序有可能难以调试，因为这些应用程序的安全权限随安装地点的不同而不同，因此其行为也各不相同。 如果从 Internet 进行安装，则部分信任的应用程序只会有极少的权限； 如果从本地 Intranet 进行安装，则会有更多的权限；如果从本地计算机安装，则会有完全权限。 您还可以有自定义区域和自定义权限。 您可能需要在以上任何一个条件或所有条件下对部分信任的应用程序进行调试。 Visual Studio 幸好也能使这些工作变得容易。  
  
 在 Visual Studio 中启动调试会话之前，可以选择模拟从哪个区域安装的应用程序。 启动调试以后，应用程序将具有某些权限，这些权限相应于从该区域安装的部分信任的应用程序。 这样，您看到的应用程序的行为就是从该区域下载应用程序的用户看到的行为。  
  
 如果应用程序尝试执行它无权执行的操作，则会发生异常。 此时，异常助手可以为您提供添加额外权限的机会，这样，您就可以具有足够的权限重新启动调试会话，以避免出现问题。  
  
 您可以在以后返回并查看自己在调试期间添加了哪些权限。 如果你在调试期间必须添加权限，则可能表示你需要在代码中相应的点添加“用户同意提示”。  
  
> [!NOTE]
> 调试器可视化工具要求比部分信任的应用程序允许的特权更大的特权。 在部分信任的代码中停止时，可视化工具不会加载。 若要使用可视化工具进行调试，必须运行完全信任的代码。  
  
### <a name="to-choose-a-zone-for-your-partial-trust-application"></a>为部分信任的应用程序选择一个区域  
  
1. 从**项目**菜单中，选择_Projectname_**属性**。  
  
2. 在中*Projectname*属性页上，单击**安全**页。  
  
3. 选择**启用 ClickOnce 安全设置**。  
  
4. 下**从中安装应用程序的区域**中，单击下拉列表框，然后选择你想要模拟从要安装的应用程序的区域。  
  
     **应用程序所需的权限**网格将显示所有可用权限。 选中标记指示授予应用程序的权限。  
  
5. 如果您选择的区域 **（自定义）**，选择正确的自定义设置中**设置**的列**权限**网格。  
  
6. 单击“确定”关闭属性页。  
  
### <a name="to-add-an-extra-permission-when-a-security-exception-occurs"></a>当发生安全异常时添加额外权限  
  
1. **异常助手**对话框中会显示消息：**SecurityException 未处理。**  
  
2. 在中**异常助手**对话框中的**操作**，单击**添加到项目的权限**。  
  
3. **重新启动调试**对话框随即出现。  
  
    - 如果你想要重新启动调试会话使用新的权限，请单击**是**。  
  
    - 如果不想要重新启动，请单击**否**。  
  
### <a name="to-view-extra-permissions-added-while-debugging"></a>查看调试时添加的额外权限  
  
1. 从**项目**菜单中，选择_Projectname_**属性**。  
  
2. 在中*Projectname*属性页上，单击**安全**页。  
  
3. 看看**应用程序所需的权限**网格。 您添加任何额外权限有两个图标**包含**列： 的正常复选标记，所有包括的权限都有该和其他图标，看上去像一个含有字母"i"的气球。  
  
4. 使用垂直滚动条来查看整个**应用程序所需的权限**网格。  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)   
 [调试器安全](../debugger/debugger-security.md)
