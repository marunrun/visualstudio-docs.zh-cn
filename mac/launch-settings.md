---
title: launchSettings.json 支持
description: 本文档介绍了 Visual Studio for Mac 中对 launchSettings.json 的支持
author: sayedihashimi
ms.author: sayedha
ms.date: 09/18/2019
ms.assetid: a556f9d7-86a8-408e-aa54-392584845889
ms.openlocfilehash: e7de368dd26bf2724a7bc060dade46422817da1e
ms.sourcegitcommit: ea182703e922c74725045afc251bcebac305068a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71213815"
---
# <a name="launchsettingsjson"></a>launchSettings.json

开发 ASP.NET Core 项目时，可以通过自定义 `launchSettings.json` 文件的内容来配置在开发场景中启动项目的方式。 在 Visual Studio for Mac 中，可以通过使用“项目选项”UI 或直接编辑 `launchSettings.json` 文件来更新此文件。 此配置文件同样可在 Windows 上运行 Visual Studio 时使用，或在使用 `dotnet` 的命令行中使用。 此文件存储在 `Properties` 文件夹下的项目中。

有关更多详细信息，请参阅[在 ASP.NET Core 中使用多种环境](https://docs.microsoft.com/aspnet/core/fundamentals/environments)。 本文档将介绍在 Visual Studio for Mac 中更新此文件的方法。

## <a name="updating-start-configuration-using-visual-studio-for-mac"></a>使用 Visual Studio for Mac 更新启动配置

可以直接在 Visual Studio for Mac 中编辑 `launchSettings.json`，也可以使用“项目选项”对其进行编辑。 若要转到“项目选项”，请右键单击项目，然后选择“选项”。 参阅下图。

![已选择的项目上下文菜单选项](media/vsmac-ctx-proj-options.png)

转到此对话框后，请前往“运行”>“配置”>“默认值”。

![运行默认配置](media/vsmac-run-config-default.png)

在此主要需要配置两项。

 - 启动时设置的环境变量
 - 项目的启动 URL

## <a name="configure-environment-variables"></a>配置环境变量

可以使用网格指定环境变量的值。 在 Visual Studio for Mac 中启动应用程序时，将设置这些环境变量。 开发 ASP.NET Core 应用程序时，应注意特殊的环境变量 `ASPNETCORE_ENVIRONMENT`。 若要了解详细信息，请参阅[在 ASP.NET Core 中使用多个环境](https://docs.microsoft.com/aspnet/core/fundamentals/environments)。


## <a name="configure-start-url"></a>配置启动 URL

要配置用于启动应用程序的 URL，请转到“ASP.NET Core”选项卡。

![proj options start url](media/vsmac-run-config-default-aspnetcore.png)

可以在此指定启动应用程序时，应用程序将侦听的 URL。