---
title: 安装 Visual Studio SDK |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: visual-studio-sdk
ms.topic: conceptual
ms.assetid: c730edb6-5099-4c16-85a8-08def09f1455
caps.latest.revision: 4
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 88a6266a3f5910def0bf5041a37f89c2b3d67416
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63414469"
---
# <a name="installing-the-visual-studio-sdk"></a>安装 Visual Studio SDK
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。  
  
## <a name="installing-the-visual-studio-sdk-as-part-of-a-visual-studio-installation"></a>作为 Visual Studio 安装的一部分安装的 Visual Studio SDK  
 如果你想要在 Visual Studio 安装中包括 VSSDK，你必须执行的自定义安装。  
  
> [!NOTE]
> 在执行安装文件，名为 Visual Studio SDK **Visual Studio 扩展性工具**。  
  
1. 启动 Visual Studio 2015 安装。 可以安装任意版本的 Visual Studio Express 除外。  
  
2. 在第一个屏幕上，选择**自定义**，而非**默认**。 单击 **“下一步”**。  
  
3. 您应看到自定义功能的树的视图。 打开**常用工具**。 应会看到**Visual Studio 扩展性工具**。  
  
     ![VSSDKInstall](../extensibility/media/vssdkinstall.png "VSSDKInstall")  
  
4. 检查**Visual Studio 扩展性工具**，然后单击**下一步**并继续安装。  
  
## <a name="installing-the-visual-studio-sdk-after-installing-visual-studio"></a>在安装 Visual Studio 后安装 Visual Studio SDK  
 如果你决定完成你的 Visual Studio 安装后安装 Visual Studio SDK，则应遵循以下过程：  
  
1. 转到**控制面板 / 程序 / 程序和功能**，并查找**Visual Studio 2015**。 可以安装适用于除 Express 之外的 Visual Studio 2015 任何版本的 Visual Studio SDK。  
  
2. 右键单击**Visual Studio 2015**，然后单击**更改**。 应看到安装页。  
  
3. 按照中的相同过程**安装 Visual Studio SDK 作为 Visual Studio 安装的一部分**上面。  
  
4. 单击**Visual Studio 扩展性工具**链接安装 Visual Studio SDK。  
  
## <a name="installing-the-visual-studio-sdk-from-a-solution"></a>从解决方案安装 Visual Studio SDK  
 如果不首先安装 VSSDK 与扩展性项目打开的解决方案，系统将提示您通过解决方案资源管理器上面突出显示的信息栏。 其外观应类似于以下内容：  
  
 ![SolutionExplorerInstall](../extensibility/media/solutionexplorerinstall.png "SolutionExplorerInstall")  
  
## <a name="installing-the-visual-studio-sdk-from-the-command-line"></a>从命令行安装 Visual Studio SDK  
 可以通过从命令行安装 VSSDK **/InstallSelectableItems**开关与 Visual Studio 安装程序。 使用命令行参数的安装程序的详细信息，请参阅[安装 Visual Studio 2015](../install/install-visual-studio-2015.md)。  
  
 下面介绍了如何安装 VSSDK 以无提示方式使用 Visual Studio 2015 Community 安装程序：  
  
```  
vs_community.exe /s /installSelectableItems VS_SDK_GROUPV1  
```  
  
 请注意，必须使用与你已安装的 Visual Studio 版本匹配的 Visual Studio 安装程序。 例如，如果必须在计算机上安装的 Visual Studio Enterprise，则必须运行 Visual Studio Enterprise 安装程序 (vs_enterprise.exe)。
