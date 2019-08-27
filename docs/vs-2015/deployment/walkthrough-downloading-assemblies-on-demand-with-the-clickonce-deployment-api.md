---
title: 演练：下载使用 ClickOnce 部署 API 按需程序集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- assemblies, downloading [ClickOnce]
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: d20e2789-8621-4806-b5b7-841122da1456
caps.latest.revision: 18
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: af03329a05501427f6d04d6cddbd637c3311b339
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63434925"
---
# <a name="walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api"></a>演练：下载使用 ClickOnce 部署 API 按需程序集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

默认情况下，所有程序集包含在[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]首次运行该应用程序时下载应用程序。 但是，您可能使用的一小组用户应用程序的部分。 在这种情况下，你希望仅当创建其类型之一时才下载程序集。 下面的演练演示如何将应用程序中的某些程序集标记为“可选”，以及如何在公共语言运行时 (CLR) 需要它们时使用 <xref:System.Deployment.Application> 命名空间中的类下载它们。  
  
> [!NOTE]
> 应用程序必须在完全信任下运行才能使用此过程。  
  
## <a name="prerequisites"></a>系统必备  
 您将需要以下组件来完成本演练之一：  
  
- Windows SDK 中。 可以从 Microsoft 下载中心下载 Windows SDK。  
  
- Visual Studio。  
  
## <a name="creating-the-projects"></a>创建项目  
  
#### <a name="to-create-a-project-that-uses-an-on-demand-assembly"></a>若要创建使用按需程序集的项目  
  
1. 创建一个名为 ClickOnceOnDemand 目录。  
  
2. 打开 Windows SDK 命令提示或[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]命令提示符。  
  
3. 将更改为 ClickOnceOnDemand 目录。  
  
4. 生成公共/专用密钥对使用以下命令：  
  
    ```  
    sn -k TestKey.snk  
    ```  
  
5. 使用记事本或其他文本编辑器中，定义一个名为类`DynamicClass`具有单个属性名为`Message`。  
  
     [!code-csharp[ClickOnceLibrary#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnceLibrary/CS/Class1.cs#1)]
     [!code-vb[ClickOnceLibrary#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceLibrary/VB/Class1.vb#1)]  
  
6. 将文本保存为文件命名`ClickOnceLibrary.cs`或`ClickOnceLibrary.vb`，取决于您使用到 ClickOnceOnDemand 目录的语言。  
  
7. 将文件编译到程序集。  
  
    ```csharp  
    csc /target:library /keyfile:TestKey.snk ClickOnceLibrary.cs  
    ```  
  
    ```vb  
    vbc /target:library /keyfile:TestKey.snk ClickOnceLibrary.vb  
    ```  
  
8. 若要获取该程序集的公钥令牌，请使用以下命令：  
  
    ```  
    sn -T ClickOnceLibrary.dll  
    ```  
  
9. 创建新的文件使用文本编辑器并输入以下代码。 此代码创建在需要时下载 ClickOnceLibrary 程序集的 Windows 窗体应用程序。  
  
     [!code-csharp[ClickOnceOnDemandCmdLine#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemandCmdLine/CS/Form1.cs#1)]
     [!code-vb[ClickOnceOnDemandCmdLine#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemandCmdLine/VB/Form1.vb#1)]  
  
10. 在代码中，找到调用<xref:System.Reflection.Assembly.LoadFile%2A>。  
  
11. 设置`PublicKeyToken`为前面检索到的值。  
  
12. 将文件保存为任一`Form1.cs`或`Form1.vb`。  
  
13. 将它编译成可执行文件使用以下命令。  
  
    ```csharp  
    csc /target:exe /reference:ClickOnceLibrary.dll Form1.cs  
    ```  
  
    ```vb  
    vbc /target:exe /reference:ClickOnceLibrary.dll Form1.vb  
    ```  
  
## <a name="marking-assemblies-as-optional"></a>将程序集标记为可选  
  
#### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-mageuiexe"></a>使用 MageUI.exe 将标记为可选 ClickOnce 应用程序中的程序集  
  
1. 使用 MageUI.exe 中，创建应用程序清单中所述[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。 对该应用程序清单中使用以下设置：  
  
    - 命名应用程序清单`ClickOnceOnDemand`。  
  
    - 上**文件**页上，在 ClickOnceLibrary.dll 行中，设置**文件类型**列**None**。  
  
    - 上**文件**页上，在 ClickOnceLibrary.dll 行中，类型`ClickOnceLibrary.dll`中**组**列。  
  
2. 使用 MageUI.exe 中，创建部署清单中所述[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。 对于部署清单中使用以下设置：  
  
    - 命名的部署清单`ClickOnceOnDemand`。  
  
## <a name="testing-the-new-assembly"></a>测试新程序集  
  
#### <a name="to-test-your-on-demand-assembly"></a>测试按需程序集  
  
1. 上传你[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署到 Web 服务器。  
  
2. 启动应用程序部署与[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]从 Web 浏览器通过输入到部署清单 URL。 如果调用你[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序`ClickOnceOnDemand`，并将其上载到 adatum.com 的根目录，你的 URL 将如下所示：  
  
    ```  
    http://www.adatum.com/ClickOnceOnDemand/ClickOnceOnDemand.application  
    ```  
  
3. 在主窗体显示时按 <xref:System.Windows.Forms.Button>。 应在消息框窗口中看到一个显示为“Hello, World!”的字符串。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Deployment.Application.ApplicationDeployment>
