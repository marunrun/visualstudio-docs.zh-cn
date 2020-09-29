---
title: GitHub Codespaces 概述（预览）
description: 了解有关带有 Visual Studio 的 GitHub Codespaces 的详细信息，以及它如何帮助将开发环境扩展到云。
ms.topic: overview
ms.date: 09/04/2020
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: vs-2019
ms.openlocfilehash: 629ad64ad2a179e1f70998240f26a4484280e514
ms.sourcegitcommit: 09d1f5cef5360cdc1cdfd4b22a1a426b38079618
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "91005008"
---
# <a name="what-is-github-codespaces-preview"></a>什么是 GitHub Codespaces？ （预览版）

欢迎使用 Codespaces！ 我们很高兴在这里遇到你。

GitHub Codespaces 为你提供了一个云支持型开发环境，可用于处理任何活动，无论该活动是长期项目，还是短期任务（如查看拉取请求）。 可在 Visual Studio 2019 Preview 中使用 codespace （[注册有限的 public beta 版本](https://github.com/features/codespaces/signup-vs)）。

此外，GitHub Codespaces 还带来了 DevOps 的许多优势，例如可重复性和可靠性，这些优势通常保留给开发环境中的生产工作负载。 你还可以个性化设置 GitHub Codespaces，以使用你喜欢和依赖的工具、进程和配置。

本文档将解释关键概念并介绍 Codespaces 功能。 如果想开始使用，请查看[将 Visual Studio 用于 codespace](use-visual-studio-with-codespaces.md)。

> [!IMPORTANT]
> 必须注册有限的 [public beta 版本](https://github.com/features/codespaces/signup-vs)才能使用 GitHub Codespaces。 在 beta 版本期间，GitHub 不保证 Codespaces 的可用性。 有关加入 beta 版本的详细信息，请参阅[关于 Codespaces](https://docs.github.com/github/developing-online-with-codespaces/about-codespaces#joining-the-beta)。

## <a name="concepts-and-features"></a>概念和功能

GitHub Codespaces 功能建立在一些基本概念之上。 本部分介绍了这些概念，并简要介绍了这些功能。

### <a name="remote-development"></a>远程开发

如今，许多开发人员都尝试在配置有特定开发和运行时堆栈的远程设置或 VM 中编写代码。 他们这样做是因为在本地设置这些开发环境极其困难、极具破坏性，在某些情况下，甚至几乎不可能实现。 此外，人们希望尝试新技术或新框架，而无需担心“弄乱”他们日常工作所需的计算机。

虽然开发人员可以使用远程环境和具有远程功能的工具提高工作效率，但这通常会产生计算机管理开销。 环境配置通常会使载入和上下文切换变得更加复杂。 GitHub Codespaces 通过允许多环境同时存在，消除了快速载入和上下文切换的障碍。 

GitHub Codespaces 提供托管解决方案，可让你专注于生产力而非设置。 GitHub Codespaces 针对远程开发从概念上和技术上扩展了 Visual Studio 2019。 

### <a name="about-codespaces"></a>关于 codespace

Codespace 是 GitHub Codespaces 的后端部分。 与软件开发相关的所有计算都在这里进行，包括编译、调试、还原等。创建 codespace 可以为完成任务、审阅 PR 或启动新项目做好一切准备。 Codespaces 可用于配置以下内容：运行时、编译器、调试程序、编辑器、自定义点文件配置及处理项目所需的源代码。

云托管的 codespace 具有以下优势：

- 创建速度快且是一次性的。 可根据需要创建任意数量（不超过帐户限制）的 codespace，然后在完成时将其清除。
- 它们是托管的，可减少整体维护。
- 价格可预测，你只需为使用的资源付费。 此外，还提供了内置的自动暂停功能，以消除失控成本。
- 节省计算资源。 将开发工作负载转移到云时，它会在个人计算机上释放有限的资源。

## <a name="custom-configuration"></a>自定义配置

GitHub Codespaces 旨在适应最广泛的项目或任务。 可以从提供常见默认设置的智能配置功能开始，也可以使用[自定义配置](customize-codespaces.md)微调 codespace。

灵活的配置使开发人员可以快速载入项目，这些项目具有难以在本地计算机上应用的独特配置和要求。 此外，可重现的 codespaces 消除了“在我的计算机上工作”的问题。

## <a name="personal-configuration"></a>个人配置

我们知道，保留个人偏好对于在云托管的 codespace 上熟悉而自然地进行开发至关重要。 GitHub Codespaces 可以在 codespace 配置的基础上对个性化自定义进行分层。 GitHub Codespaces 支持编辑器和终端的个人偏好和配置。

可以使用特定于用户的[自定义点文件](https://docs.github.com/github/developing-online-with-codespaces/personalizing-codespaces-for-your-account)（例如 `.bashrc`、`.gitconfig` 等）集合来创建 codespace，GitHub Codespaces 会自动同步你的 Git 标识、主题和设置，以便无论特定于项目的环境功能如何，你创建的每个 codespace 都能具有你喜欢的外观和感受。

## <a name="see-also"></a>另请参阅

* [如何将 Visual Studio 用于 codespace](use-visual-studio-with-codespaces.md)
* [如何自定义 codespace](customize-codespaces.md)
* [受支持的 Visual Studio 功能](supported-features-codespaces.md)
