---
title: 安装 Visual Studio SDK | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: visual-studio-sdk
ms.topic: conceptual
ms.assetid: c730edb6-5099-4c16-85a8-08def09f1455
caps.latest.revision: 4
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 88a6266a3f5910def0bf5041a37f89c2b3d67416
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841328"
---
# <a name="installing-the-visual-studio-sdk"></a>安装 Visual Studio SDK
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 也可稍后安装 VS SDK。  
  
## <a name="installing-the-visual-studio-sdk-as-part-of-a-visual-studio-installation"></a>安装 visual studio SDK 作为 Visual Studio 安装的一部分  
 如果要在 Visual Studio 安装中包含 VSSDK，则必须执行自定义安装。  
  
> [!NOTE]
> 在安装可执行文件中，Visual Studio SDK **Visual Studio 扩展性工具**调用。  
  
1. 启动 Visual Studio 2015 安装。 可以安装任何版本的 Visual Studio （Express 除外）。  
  
2. 在第一个屏幕上，选择 " **自定义**，而不是 **默认值**"。 单击“下一步”。  
  
3. 应会看到自定义功能的树状视图。 打开 **常用工具**。 应会看到 **Visual Studio 扩展性工具** 。  
  
     ![VSSDKInstall](../extensibility/media/vssdkinstall.png "VSSDKInstall")  
  
4. 选中 **Visual Studio 扩展性工具** ，然后单击 " **下一步** " 继续安装。  
  
## <a name="installing-the-visual-studio-sdk-after-installing-visual-studio"></a>安装 visual Studio 后安装 Visual Studio SDK  
 如果你决定在完成 Visual Studio 安装后安装 Visual Studio SDK，则应执行以下过程：  
  
1. 请参阅 **"控制面板"/"程序"/"程序和功能**"，并查找 **Visual Studio 2015**。 对于 Visual Studio 2015 的任意版本，你可以安装 Visual Studio SDK （Express 除外）。  
  
2. 右键单击 " **Visual Studio 2015**"，然后单击 " **更改**"。 应会看到 "安装" 页。  
  
3. 按照上面的 **Visual Studio 安装的一部分安装 Visual STUDIO SDK** 中所述的相同过程进行操作。  
  
4. 单击 " **Visual Studio 扩展性工具** " 链接以安装 VISUAL Studio SDK。  
  
## <a name="installing-the-visual-studio-sdk-from-a-solution"></a>从解决方案安装 Visual Studio SDK  
 如果在未首先安装 VSSDK 的情况下使用扩展性项目打开解决方案，则会通过解决方案资源管理器上方突出显示的信息栏来提示您。 它应该如下所示：  
  
 ![SolutionExplorerInstall](../extensibility/media/solutionexplorerinstall.png "SolutionExplorerInstall")  
  
## <a name="installing-the-visual-studio-sdk-from-the-command-line"></a>从命令行安装 Visual Studio SDK  
 可以通过在 Visual Studio 安装程序中使用 **/InstallSelectableItems** 开关，从命令行安装 VSSDK。 有关使用安装程序的命令行参数的详细信息，请参阅 [安装 Visual Studio 2015](../install/install-visual-studio-2015.md)。  
  
 下面介绍如何使用 Visual Studio 2015 社区安装程序以无提示方式安装 VSSDK：  
  
```  
vs_community.exe /s /installSelectableItems VS_SDK_GROUPV1  
```  
  
 请注意，必须使用与已安装的 Visual Studio 版本匹配的 Visual Studio 安装程序。 例如，如果计算机上安装了 Visual Studio Enterprise，则必须运行 Visual Studio Enterprise 安装程序 (vs_enterprise.exe)。
