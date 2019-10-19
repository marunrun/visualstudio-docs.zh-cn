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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5c11c952223854ff1b4b963e24615e7abe831496
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669863"
---
# <a name="deploy-a-layer-model-extension"></a>部署层模型扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

其他 Visual Studio 用户可通过使用 Visual Studio 安装你创建的层建模扩展。

## <a name="installing-your-extension"></a>安装你的扩展
 将你的扩展编译为可在其他计算机上安装的 VSIX 文件。 你也可以将其安装到开发计算机，确保该扩展在 Visual Studio 的主实例中可用。

#### <a name="to-install-the-extension"></a>安装扩展

1. 在包含**源 .vsix 清单**的项目中，打开 "文件资源管理器" 中的 " **\\ \\** "。

2. 将 **\* .vsix**文件复制到要安装该扩展的计算机。

3. 在目标计算机的 Windows 资源管理器中，双击 *.vsix 文件。

    VSIX 安装程序将打开。

#### <a name="to-uninstall-the-extension"></a>卸载扩展

1. 在 Visual Studio 的 "**工具**" 菜单上，单击 "**扩展和更新**"。

2. 单击扩展的名称，然后单击 "**卸载**"。

## <a name="installing-an-extension-on-a-team-foundation-build-server"></a>在 Team Foundation Build 服务器上安装扩展
 通常情况下，[!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 服务器并未安装 Visual Studio，因此无法通过对其双击来安装 VSIX。 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 的安装包括一些允许运行 VSIX 扩展的组件，但你必须手动安装该扩展。

#### <a name="to-install-your-layer-extension-on-a-includeesprbuildincludesesprbuild-mdmd-server"></a>在 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 服务器上安装层扩展

1. 将 **.vsix**文件从开发计算机复制到 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 计算机。

     将 VSIX 文件置于下列位置之一：

    - 为所有用户和服务安装：

         %ProgramFiles%\Microsoft Visual Studio [version]\Common7\IDE\Extensions\Microsoft

    - 仅为运行 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 的网络服务安装：

         %WinDir%\ServiceProfiles\NetworkService\AppData\Local\Microsoft\VisualStudio \\ [version] \Extensions\Microsoft

    - 如果你已将 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 配置为在交互模式下以特定用户身份运行，则你可以仅为该用户安装：

         %LocalAppData%\Microsoft\VisualStudio \\ [version] \Extensions\Microsoft

        > [!NOTE]
        > % LocalAppData% 通常为*DriveName*： Users*UserName*AppDataLocal。

2. 将各个 VSIX 文件展开至相同位置的文件夹中：

    1. 将文件扩展名从 **.vsix**改为 **.zip**。

    2. 将 .zip 文件中的内容提取到一个文件夹中。

    3. 删除 .zip 文件。

3. 重新启动 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)]。
