---
title: “属性页”->“JavaScript”| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- javascript.project.property.debugging.debuggertype
- javascript.project.property.debugging.requireauthentication
- javascript.project.property.outputpath
- javascript.project.property.debugging.launchapplication
- javascript.project.property.defaultlanguage
- javascript.project.property.debugging.machinename
- javascript.project.property.debugging.allowlocalnetworkloopback
ms.assetid: a05ab01f-3d5d-4675-a845-eab51807d3a3
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e9fa22a4ed52c3e0a1afdda0105716c0de9b3316
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851814"
---
# <a name="property-pages-javascript"></a>属性页，JavaScript
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

“属性页”提供对项目设置的访问。 可使用“属性页”中显示的页面来更改项目属性。

 若要访问项目属性，请在“解决方案资源管理器”中选择项目节点。 在“项目”菜单上，单击“属性”。

 [!INCLUDE[note_settings_general](../../includes/note-settings-general-md.md)]

 以下页面和选项显示在“属性页”中。

## <a name="configuration-and-platform-page"></a>配置和平台页
 使用以下选项选择要显示或修改的配置和平台。

 **配置**指定要显示或修改的配置设置。 这些设置包括“调试”（默认）、“版本”、“所有配置”或用户定义的配置。 有关详细信息，请参阅[调试和发布项目配置](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e)。

 **平台**指定要显示或修改的平台设置。 这些设置包括“任何 CPU”（[!INCLUDE[win8_appname_long](../../includes/win8-appname-long-md.md)] 应用的默认值）、“x64”、“ARM”、“x86”或用户定义的平台。 有关详细信息，请参阅[调试和发布项目配置](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e)。

## <a name="general-page"></a>常规页
 使用以下选项来设置项目的常规属性。

> [!NOTE]
> 某些选项仅在 Windows 应用商店应用程序中可用。

 **输出路径**指定项目配置的输出文件的位置。 该路径是相对；如果输入绝对路径，绝对路径会保存在项目中。 默认路径为 bin\Debug。

 当使用简化的生成配置时，项目系统将确定是生成调试版本还是发行版本。 单击“调试”、“启动调试”（或按 F5）时，会将生成放在调试位置，而不考虑你指定的“输出路径”。 但是，“生成”菜单上的“生成解决方案”命令会将其放在指定的位置。 若要启用高级生成配置，请在菜单栏上，依次选择“工具”、“选项”。 在“选项”对话框中，展开“项目和解决方案”，选择“常规”，然后清除“显示高级生成配置”复选框。 这样，你便可以手动控制所有配置值，并控制是生成调试版本还是发行版本。 有关详细信息，请参阅[钢笔：常规、项目和解决方案、选项对话框](https://msdn.microsoft.com/8f8e37e8-b28d-4b13-bfeb-ea4d3312aeca)。

 **默认语言**指定项目的默认语言。 在控制面板中的“时钟、语言和区域”中选中的语言选项可指定用户的首选语言。 如果用户的首选语言与应用程序中提供的语言资源不匹配，可通过指定项目的默认语言，确保使用指定的默认语言资源。

## <a name="debug-page"></a>调试页
 使用以下选项来设置项目中调试行为的属性。

> [!NOTE]
> 某些选项仅在 Windows 应用商店应用程序中可用。

 **要启动的调试器**指定调试器的默认主机。

- 选择“本地计算机”可在 Visual Studio 主机计算机上启动应用程序。 有关详细信息，请参阅[在本地计算机上运行应用](https://msdn.microsoft.com/library/windows/apps/hh441483(v=VS.85).aspx)。

- 选择“模拟器”可在模拟器中启动应用程序。 有关详细信息，请参阅[在模拟器中运行应用](https://msdn.microsoft.com/library/windows/apps/hh441475(v=VS.85).aspx)。

- 选择“远程计算机”可在远程计算机上启动应用程序。 有关远程调试的详细信息，请参阅[在远程计算机上运行应用](https://msdn.microsoft.com/library/windows/apps/hh441469(v=VS.85).aspx)。

  **启动应用程序**指定在按 F5 或单击 "**调试**"、"**启动调试**" 时是否启动应用程序。 选择“是”则启动应用程序；否则，请选择“否”。 如果选择“否”，而使用另一种方法来启动，则仍然可以调试应用程序。

  **调试器类型**指定要调试的代码类型。 选择“仅限脚本”可调试 JavaScript 代码。 选择“仅限托管”可调试由公共语言运行时托管的代码。 选择“仅限本机”可调试 C++ 代码。 选择“本机(带脚本)”可调试 C++ 和 JavaScript。 选择“混合(托管和本机)”可调试托管代码和 C++ 代码。

  **允许本地网络环回**指定是否允许对 IP 环回地址进行访问以进行应用测试。 如果客户端应用位于运行服务器应用程序的同一台计算机上，请选择“是”，允许使用环回地址；否则，请选择“否”。 此属性仅当“要启动的调试器”属性设置为“远程计算机”时可用。

  **计算机名称**指定要承载调试器的远程计算机的名称。 此属性仅当“要启动的调试器”设置为“远程计算机”时可用。

  **要求身份验证**指定远程计算机是否需要身份验证。 此属性仅当“要启动的调试器”设置为“远程计算机”时可用。
