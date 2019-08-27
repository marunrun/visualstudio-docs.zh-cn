---
title: 部署层模型扩展 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- layer diagrams, deploying extensions
- layer models, deploying extensions
ms.assetid: 00a4675b-d20e-487e-8fd5-be2b1e0ba238
caps.latest.revision: 29
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a58adf1be92655a6ca7846e8c1d7ea41515b7109
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63422665"
---
# <a name="deploy-a-layer-model-extension"></a>部署层模型扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

其他 Visual Studio 用户可通过使用 Visual Studio 安装你创建的层建模扩展。  
  
## <a name="installing-your-extension"></a>安装你的扩展  
 将你的扩展编译为可在其他计算机上安装的 VSIX 文件。 你也可以将其安装到开发计算机，确保该扩展在 Visual Studio 的主实例中可用。  
  
#### <a name="to-install-the-extension"></a>安装扩展  
  
1. 中包含的项目**source.vsix.manifest**，打开**bin\\\\*** 在文件资源管理器。  
  
2. 复制 **\*.vsix**到要安装扩展的计算机的文件。  
  
3. 在目标计算机的 Windows 资源管理器中，双击 *.vsix 文件。  
  
    VSIX 安装程序将打开。  
  
#### <a name="to-uninstall-the-extension"></a>卸载扩展  
  
1. 在 Visual Studio 中，在**工具**菜单上，单击**扩展和更新**。  
  
2. 单击扩展的名称，然后单击**卸载**。  
  
## <a name="installing-an-extension-on-a-team-foundation-build-server"></a>在 Team Foundation Build 服务器上安装扩展  
 通常情况下，[!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 服务器并未安装 Visual Studio，因此无法通过对其双击来安装 VSIX。 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 的安装包括一些允许运行 VSIX 扩展的组件，但你必须手动安装该扩展。  
  
#### <a name="to-install-your-layer-extension-on-a-includeesprbuildincludesesprbuild-mdmd-server"></a>在 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 服务器上安装层扩展  
  
1. 复制 **.vsix**文件从开发计算机[!INCLUDE[esprbuild](../includes/esprbuild-md.md)]计算机。  
  
     将 VSIX 文件置于下列位置之一：  
  
    - 为所有用户和服务安装：  
  
         %ProgramFiles%\Microsoft Visual Studio [version]\Common7\IDE\Extensions\Microsoft  
  
    - 仅为运行 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 的网络服务安装：  
  
         %WinDir%\ServiceProfiles\NetworkService\AppData\Local\Microsoft\VisualStudio\\[version]\Extensions\Microsoft  
  
    - 如果你已将 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 配置为在交互模式下以特定用户身份运行，则你可以仅为该用户安装：  
  
         %LocalAppData%\Microsoft\VisualStudio\\[version]\Extensions\Microsoft  
  
        > [!NOTE]
        > %Localappdata%通常是*DriveName*： 用户*用户名*AppDataLocal。  
  
2. 将各个 VSIX 文件展开至相同位置的文件夹中：  
  
    1. 更改文件扩展名，从 **.vsix**到 **.zip**。  
  
    2. 将 .zip 文件中的内容提取到一个文件夹中。  
  
    3. 删除 .zip 文件。  
  
3. 重新启动 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)]。
