---
title: 管理项目中的引用
description: 本文介绍如何在 Visual Studio for Mac 中管理项目中的引用
author: jmatthiesen
ms.author: jomatthi
ms.date: 05/06/2018
ms.assetid: 4AD51385-B0A8-4BA7-B2D4-BF2BD167A142
ms.openlocfilehash: a14630c5448632a939e1768040b910caf6276c2a
ms.sourcegitcommit: 7fbfb2a1d43ce72545096c635df2b04496b0be71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67692922"
---
# <a name="managing-references-in-a-project"></a>管理项目中的引用

Visual Studio for Mac 提供了两种将其他引用添加到项目的方法：

![项目引用](media/projects-and-solutions-image10.png)

这些是：

* reference
* NuGets（通过包文件夹添加）

此外，也可将 Web 引用和本机引用添加到任何项目。

## <a name="assembly-references"></a>程序集引用

Xamarin 中的每个框架都附带十几个程序集。 项目中不会默认引用所有这些程序集包。

要编辑项目中引用的包，请使用“编辑引用”对话框，要显示该对话框，请双击引用文件夹，或在其上下文菜单操作上选择“编辑引用”   ：

![程序集引用对话框](media/projects-and-solutions-image11.png)

有关每个 Xamarin 框架可用的程序集的信息，请参阅[可用程序集](https://developer.xamarin.com/guides/cross-platform/advanced/available-assemblies/)指南。

## <a name="nuget"></a>NuGet

NuGet 是 .NET 开发最常用的程序包管理器。 通过 Visual Studio for Mac 的 NuGet 支持，可搜索要添加到项目的包。

为此，请右键单击“包”文件夹，然后选择“添加包”  。

[在项目中包括 NuGet 包](nuget-walkthrough.md)演练中提供了有关使用 NuGet 包的详细信息。

## <a name="see-also"></a>请参阅

- [管理引用（Windows 上的 Visual Studio）](/visualstudio/ide/managing-references-in-a-project)
- [使用 NuGet 添加引用与使用扩展 SDK 添加引用（Windows 上的 Visual Studio）](/visualstudio/ide/adding-references-using-nuget-versus-an-extension-sdk)