---
title: 在防火墙或代理服务器后面安装和使用 Visual Studio for Mac
description: 本文档列出了必须在防火墙中允许的主机，以便 Visual Studio for Mac（及其工作负载，包括 Xamarin）能够在企业环境中正常运行。
ms.topic: troubleshooting
ms.assetid: 79C0F1A3-0C13-4E55-A820-1138A4082B77
author: asb3993
ms.author: amburns
ms.date: 10/23/2018
ms.openlocfilehash: 446baf89dacfe7b742e3da3307711435495c8da4
ms.sourcegitcommit: 91c7f1b525e0c22d938bc4080ba4ceac2483474f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2019
ms.locfileid: "67033195"
---
# <a name="install-and-use-visual-studio-for-mac-behind-a-firewall-or-proxy-server"></a>在防火墙或代理服务器后面安装和使用 Visual Studio for Mac

如果你或贵组织使用防火墙或代理服务器等安全措施，则会有可能需要将其添加到“允许列表”的域，以及可能需要打开的端口和协议，以便在安装和使用 Visual Studio for Mac 以及 Azure 服务时获得最佳体验。

- [安装 Visual Studio for Mac](#install-visual-studio-for-mac)  ：这些表包括必须允许连接的域，以便你有权访问 Visual Studio for Mac 的所有功能和工作负载。

- [使用 Visual Studio for Mac](#use-visual-studio-for-mac)  ：这些包包括必须允许连接的域，以便你有权访问相关功能。

## <a name="install-visual-studio-for-mac"></a>安装 Visual Studio for Mac

由于 Visual Studio for Mac 安装程序从各种域和下载服务器中下载内容，因此建议在配置中将这些域和 URL 添加为受信任的域和 URL。

### <a name="microsoft-domains"></a>Microsoft 域

| Domain| 目标 |
| ----------------------------------- |---------------------------|
| *.live.com| 凭据管理 |
| app.vssps.visualstudio.com| 安装程序元数据|
| vortex.data.microsoft.com | 故障和错误报告 |
| az667904.vo.msecnd.net| 故障和错误报告 |
| xamarin.com | 安装程序元数据|
| xampubdl.blob.core.windows.net| 安装程序包|
| download.visualstudio.microsoft.com | 安装程序包|
| xamarin.azureedge.net | 安装程序包|
| developer.xamarin.com | 安装程序包|
| dc.services.visualstudio.com| 故障报告 |

### <a name="third-party-domains"></a>第三方域

| Domain| 目标 |
| --------------------------|-------------------------|
| dl.google.com | Android SDK |
| download.oracle.com | Java SDK|
| api.apple-cloudkit.com| Apple 安全服务 |

## <a name="use-visual-studio-for-mac"></a>使用 Visual Studio for Mac

为了确保你有权在代理或防火墙后面访问 Visual Studio for Mac 中所需每个功能，建议将以下域和端口添加到允许的访问列表。

### <a name="general"></a>常规

| Domain | 端口|目标|
| ----------------------|------------------|------------------|
| go.microsoft.com | 80/443|Microsoft URL 解析 |
| vsstartpage.blob.core.windows.net| 80/443| 起始页数据|
| software.xamarin.com |  80/443|更新程序服务|
| addins.monodevelop.com | 80/443| 扩展服务 |
| visualstudio-devdiv-c2s.msedge.net | 80/443| 试验功能和通知 |
| targetednotifications.azurewebsites.net|  80/443| 用于将全局通知列表筛选为一个仅适用于特定类型计算机/使用方案的列表|

### <a name="identity"></a>标识

| Domain | 端口|目标|
| ----------------------|------------------|------------------|
| login.microsoftonline.com | 80/443| 标识提供程序|
| secure.aadcdn.microsoftonline-p.com | 80/443|标识提供程序|
| dc.services.visualstudio.com| 80/443|故障报告|
| management.azure.com|80/443| Azure 服务 API |

### <a name="nuget"></a>NuGet

| Domain | 端口|目标|
| ----------------------|------------------|------------------|
| api.nuget.org | 80/443|NuGet API|
| secure.aadcdn.microsoftonline-p.com |80/443| 标识提供程序|

### <a name="android-projects"></a>Android 项目

| Domain| 目标|
| ------------------------------------|------------------------------------|
| time.android.com| Android Emulator 时间服务器 |
| connectivitycheck.gstatic.com | Android Emulator 连接性|
| cloudconfig.googleapis.com| Android Emulator API|

## <a name="see-also"></a>请参阅

- [在防火墙或代理服务器后面安装和使用 Visual Studio 2017 和 Azure 服务](/visualstudio/install/install-and-use-visual-studio-behind-a-firewall-or-proxy-server)
- [在 Windows 上排查类似问题](/visualstudio/install/troubleshooting-network-related-errors-in-visual-studio)
