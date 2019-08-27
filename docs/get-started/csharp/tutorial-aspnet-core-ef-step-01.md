---
title: 使用实体框架和 Visual Studio 2019 创建 ASP.NET Core Web 应用
titleSuffix: ''
description: 在创建 ASP.Net Core Web 应用之前，请先了解如何通过本视频教程和分步说明安装 Visual Studio 2019。
ms.custom: get-started
ms.date: 03/31/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
monikerRange: vs-2019
ms.topic: tutorial
ms.devlang: CSharp
author: ardalis
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: 6668648668ab71e033d1341d71ecf5c7c2a47554
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66261725"
---
# <a name="tutorial-create-your-first-aspnet-core-app-using-entity-framework-with-visual-studio-2019"></a>教程：使用实体框架和 Visual Studio 2019 创建首个 ASP.NET Core 应用

在本教程中，将创建使用数据的 ASP.NET Core Web 应用，并将其部署到 Azure。 本教程包含以下几个步骤：

- [步骤 1：安装 Visual Studio 2019](#step-1-install-visual-studio-2019)
- [步骤 2：创建首个 ASP.NET Core Web 应用](tutorial-aspnet-core-ef-step-02.md)
- [步骤 3：使用实体框架处理数据](tutorial-aspnet-core-ef-step-03.md)
- [步骤 4：从 ASP.NET Core 应用中公开 Web API](tutorial-aspnet-core-ef-step-04.md)
- [步骤 5：将 ASP.NET Core 应用部署到 Azure](tutorial-aspnet-core-ef-step-05.md)

## <a name="step-1-install-visual-studio-2019"></a>步骤 1：安装 Visual Studio 2019

了解如何使用此视频教程和分步说明安装 Visual Studio 2019。 如果已安装 Visual Studio，请跳到[步骤 2：创建首个 ASP.NET Core Web 应用](tutorial-aspnet-core-ef-step-02.md)。

观看本视频，按照说明安装 Visual Studio 并创建首个 ASP.NET Core 应用。

> [!VIDEO https://www.youtube.com/embed/Fz_HAqQGLtY]

## <a name="download-the-installer"></a>下载安装程序

转到 [visualstudio.com](https://visualstudio.com) 以找到安装程序。 找到 Visual Studio 2019 链接，单击以开始下载。 对于 Visual Studio 的免费版本，请选择“Visual Studio Community”。

## <a name="start-the-installer"></a>启动安装程序

完成下载后，单击“运行”以启动安装程序。

![Visual Studio 2019 安装程序](media/vs-2019/vs2019-installer.png)

## <a name="choose-workloads"></a>选择工作负载

Visual Studio 可用于许多不同类型的开发，工作负载使你可以轻松下载想要生成的应用类型所需的所有内容。 目前选择“ASP.NET 和 Web 开发”以及“.NET Core 跨平台开发”工作负载。 稍后始终可以通过重新启动安装程序来安装其他的工作负载和组件。

![Visual Studio 2019 选择工作负载](media/vs-2019/vs2019-choose-workloads.png)

## <a name="install"></a>安装

单击“安装”并让安装程序下载并安装 Visual Studio。

## <a name="run-visual-studio-for-the-first-time"></a>第一次运行 Visual Studio

安装程序完成后，Visual Studio 应会自动启动。 系统可能会提示你登录，其中包含一些与之关联的不错的功能，但现在可以选择稍后登录。 接下来可以选择主题和开发设置。 进行这些选择之后，即可准备好开始你的首个项目。 单击“创建新项目”，然后选择“ASP.NET Core Web 应用程序”。

![Visual Studio 2019 创建新 ASP.NET Core Web 应用程序项目](media/vs-2019/vs2019-create-new-project.png)

## <a name="explore-aspnet-core-project-types"></a>了解 ASP.NET Core 项目类型

可以选择项目名称和位置，然后选取“创建”。 现在，选择要用于 ASP.NET Core 应用程序的模板。 可从以下选项中进行选择：

- 空。 可从零开始的空项目模板。
- API。 最适合 Web API。
- Web 应用程序。 使用 Razor Pages 生成的标准 ASP.NET Core Web 应用程序。
- Web 应用程序（模型-视图-控制器）。 使用模型-视图-控制器模式的标准 ASP.NET Core Web 应用程序。
- Angular。
- React.js。
- React.js / Redux。
- Razor 类库。 用于在项目之间共享 Razor 资产。

请注意，对于大多数项目模板，还可以通过选中一个框来启用 Docker 支持。 此外可以通过单击“更改身份验证”按钮来添加身份验证支持。 可以从中选择下列项目：

- 不进行身份验证。
- 个人用户帐户。 这些存储在本地或基于 Azure 的数据库。
- 工作或学校帐户。 此选项使用 Active Directory、Azure AD 或 Office 365 进行身份验证。
- Windows 身份验证。 适用于 Intranet 应用程序。

选择无身份验证的标准 Web 应用程序模板，然后单击“确定”。

![Visual Studio 2019 选择 ASP.NET Core 项目选项](media/vs-2019/vs2019-choose-aspnetcore-project.png)

## <a name="next-steps"></a>后续步骤

在下一个视频中，你将了解有关首个 ASP.NET Core 项目的详细信息。

[教程：创建首个 ASP.NET Core Web 应用](tutorial-aspnet-core-ef-step-02.md)

## <a name="see-also"></a>请参阅

- [教程：C# 和 ASP.NET Core 入门](tutorial-aspnet-core.md)，该教程更为详细，无需视频演练
