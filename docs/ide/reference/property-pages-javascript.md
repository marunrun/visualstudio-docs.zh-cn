---
title: 属性页，JavaScript
ms.date: 06/21/2017
ms.technology: vs-javascript
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6883e556cd70adddd45fd442d338e10d1cafa1e2
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "68926197"
---
# <a name="property-pages-javascript"></a>属性页，JavaScript

“属性页”提供对项目设置的访问  。 可使用“属性页”中显示的页面来更改项目属性  。

若要访问项目属性，请在“解决方案资源管理器”中选择项目节点  。 在 **“项目”** 菜单上，单击 **“属性”** 。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

以下页面和选项显示在“属性页”中  。

## <a name="configuration-and-platform-page"></a>配置和平台页

使用以下选项选择要显示或修改的配置和平台。

 **配置**

指定要显示或修改的配置设置。 这些设置包括“调试”（默认）、“版本”、“所有配置”或用户定义的配置    。 有关详细信息，请参阅[如何：在 Visual Studio 中设置调试和发布配置](../../debugger/how-to-set-debug-and-release-configurations.md)。

 **平台**

指定要显示或修改的平台设置。 这些设置包括“任何 CPU”（ **应用的默认值）、“x64”、“ARM”、“x86”或用户定义的平台**[!INCLUDE[win8_appname_long](../../debugger/includes/win8_appname_long_md.md)]    。 有关详细信息，请参阅[如何：在 Visual Studio 中设置调试和发布配置](../../debugger/how-to-set-debug-and-release-configurations.md)。

## <a name="general-page"></a>“常规”页

使用以下选项来设置项目的常规属性。

> [!NOTE]
> 某些选项仅可用于 UWP 应用。

 输出路径 

指定项目的配置的输出文件的位置。 该路径是相对；如果输入绝对路径，绝对路径会保存在项目中。 默认路径为 bin\Debug。

当使用简化的生成配置时，项目系统将确定是生成调试版本还是发行版本。 单击“调试” **“启动调试”（或按 F5）时，会将生成放在调试位置，而不考虑你指定的“输出路径”**  >     。 但是，“生成”菜单上的“生成解决方案”命令会将其放在指定的位置   。 要启用高级生成配置，请在菜单栏上，依次选择“工具” **“选项”**  >   。 在“选项”对话框中，展开“项目和解决方案”，选择“常规”，然后清除“显示高级生成配置”复选框     。 这样，你便可以手动控制所有配置值，并控制是生成调试版本还是发行版本。

 默认语言 

指定项目的默认语言。 在控制面板中的“时钟、语言和区域”中选中的语言选项可指定用户的首选语言  。 如果用户的首选语言与应用程序中提供的语言资源不匹配，可通过指定项目的默认语言，确保使用指定的默认语言资源。

## <a name="debug-page"></a>调试页

使用以下选项来设置项目中调试行为的属性。

> [!NOTE]
> 某些选项仅可用于 UWP 应用。

 要启动的调试器 

指定调试器的默认主机。

- 选择“本地计算机”可在 Visual Studio 主机计算机上启动应用程序  。 有关详细信息，请参阅[在本地计算机上运行应用](../../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)。

- 选择“模拟器”可在模拟器中启动应用程序  。 有关详细信息，请参阅[在模拟器中运行应用](../../debugger/run-windows-store-apps-in-the-simulator.md)。

- 选择“远程计算机”可在远程计算机上启动应用程序  。 有关远程调试的详细信息，请参阅[在远程计算机上运行应用](../../debugger/run-windows-store-apps-on-a-remote-machine.md)。

启动应用程序 

指定按 F5 或依次单击“调试” **“启动调试”时是否启动应用程序**   >   。 选择“是”则启动应用程序；否则，请选择“否”   。 如果选择“否”，而使用另一种方法来启动，则仍然可以调试应用程序  。

调试器类型 

指定要调试的代码的类型。 选择“仅限脚本”可调试 JavaScript 代码  。 选择“仅限托管”可调试由公共语言运行时托管的代码  。 选择“仅限本机”可调试 C++ 代码  。 选择“本机(带脚本)”可调试 C++ 和 JavaScript  。 选择“混合(托管和本机)”可调试托管代码和 C++ 代码  。

**允许本地网络环回**

指定是否允许应用测试访问 IP 环回地址。 如果客户端应用位于运行服务器应用程序的同一台计算机上，请选择“是”，允许使用环回地址；否则，请选择“否”   。 此属性仅当“要启动的调试器”属性设置为“远程计算机”时可用   。

计算机名称 

指定远程计算机的名称，以承载调试器。 此属性仅当“要启动的调试器”设置为“远程计算机”时可用   。

要求身份验证 

指定远程计算机是否需要身份验证。 此属性仅当“要启动的调试器”设置为“远程计算机”时可用   。
