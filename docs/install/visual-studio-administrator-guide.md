---
title: Visual Studio 管理员指南
titleSuffix: ''
description: 详细了解如何在企业环境中部署 Visual Studio。
ms.date: 03/09/2020
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
ms.assetid: 4af353f5-6cfd-4ebe-bcfb-f42306e451a0
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: bda9a73a7a1aabb2d288653ff4d7b20b1c40db8c
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79190273"
---
# <a name="visual-studio-administrator-guide"></a>Visual Studio 管理员指南

在企业环境中，系统管理员通常会从网络共享或通过使用系统管理软件向最终用户部署安装。 我们精心设计了 Visual Studio 安装程序引擎，使系统管理员可以创建网络安装位置、预配置安装默认值、在安装过程中部署产品密钥以及管理成功推出的产品更新，从而支持企业部署。

本管理员指南通过各种情境，提供有关在网络环境中进行企业部署的指导。

## <a name="before-you-begin"></a>在开始之前

在组织内部署 Visual Studio 之前，需作出几项决策，完成几项任务：

::: moniker range="vs-2019"

* 确保每台目标计算机满足[最低安装要求](/visualstudio/releases/2019/system-requirements/)。

* 确定服务需求。

  如果公司需要继续使用某一功能集，但仍想获取常规维护更新，请计划使用维护基线。 有关详细信息，请参阅 [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing#support-options-for-enterprise-and-professional-customers)页面的“Enterprise 和 Professional 客户的支持选项”部分以及[如何：在维修基线上更新 Visual Studio](update-servicing-baseline.md) 页面。

  如果打算应用维护更新及累积功能更新，可选择最新的位数。

* 确定更新模型。

  希望单个客户端计算机在哪里获得更新？ 具体而言，确定是想要从 Internet 还是从公司范围的本地共享获取更新。 接下来，如果选择使用本地共享，确定是单个用户可以自行更新客户端，还是需要管理员以编程方式更新客户端。

* 确定公司所需的[工作负载和组件](workload-and-component-ids.md?view=vs-2019)。

* 确定是否使用[响应文件](automated-installation-with-response-file.md?view=vs-2019)（这可简化脚本文件中的管理细节）。

* 确定是否要启用组策略，以及是否要在个人计算机上将 Visual Studio 配置为禁用客户反馈。

::: moniker-end

::: moniker range="vs-2017"

* 确保每台目标计算机满足[最低安装要求](/visualstudio/productinfo/vs2017-system-requirements-vs/)。

* 确定服务需求。

  如果公司需要继续使用某一功能集，但仍想获取常规维护更新，请计划使用维护基线。 有关详细信息，请参阅 [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing#support-for-older-versions-of-visual-studio)页面的“对较旧版本的 Visual Studio 的支持”部分以及[如何：在维修基线上更新 Visual Studio](update-servicing-baseline.md) 页面。

  如果打算应用维护更新及累积功能更新，可选择最新的位数。

* 确定更新模型。

  希望单个客户端计算机在哪里获得更新？ 具体而言，确定是想要从 Internet 还是从公司范围的本地共享获取更新。 接下来，如果选择使用本地共享，确定是单个用户可以自行更新客户端，还是需要管理员以编程方式更新客户端。

* 确定公司所需的[工作负载和组件](workload-and-component-ids.md?view=vs-2017)。

* 确定是否使用[响应文件](automated-installation-with-response-file.md?view=vs-2017)（这可简化脚本文件中的管理细节）。

* 确定是否要启用组策略，以及是否要在个人计算机上将 Visual Studio 配置为禁用客户反馈。

::: moniker-end

::: moniker range="vs-2019"

## <a name="step-1---download-visual-studio-product-files"></a>第 1 步 - 下载 Visual Studio 产品文件

* [选择要安装的工作负载和组件](workload-and-component-ids.md?view=vs-2019)。

* [创建 Visual Studio 产品文件的网络共享](create-a-network-installation-of-visual-studio.md?view=vs-2019)。

## <a name="step-2---build-an-installation-script"></a>第 2 步 - 生成安装脚本

* 生成使用[命令行参数](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019)来控制安装的安装脚本。

  >[!NOTE]
  > 可通过使用[响应文件](automated-installation-with-response-file.md?view=vs-2019)来简化脚本。 确保创建包含默认安装选项的响应文件。

* （可选）[应用批量许可证产品密钥](automatically-apply-product-keys-when-deploying-visual-studio.md?view=vs-2019)作为安装脚本的一部分，这样用户便无需单独激活软件。

* （可选）将网络布局更新为[控制何时何地向最终用户提供产品更新](controlling-updates-to-visual-studio-deployments.md?view=vs-2019)。

* （可选）设置影响 Visual Studio 部署的注册表策略，例如与其他版本或实例共享的一些包的安装位置、[缓存包的位置](set-defaults-for-enterprise-deployments.md?view=vs-2019)或[是否缓存包](disable-or-move-the-package-cache.md?view=vs-2019)。

* （可选）设置组策略。 还可在个人计算机上[将 Visual Studio 配置为禁用客户反馈](../ide/visual-studio-experience-improvement-program.md)。

## <a name="step-3---deploy"></a>第 3 步 - 部署

* 使用所选部署技术，在目标开发者工作站上执行脚本。

## <a name="step-4---deploy-updates"></a>第 4 步 - 部署更新

* 定期运行第 1 步中的命令来添加更新后的组件，使用 Visual Studio [最新更新刷新网络位置](update-a-network-installation-of-visual-studio.md?view=vs-2019)。

  可以使用更新脚本来更新 Visual Studio。 为此，请使用 [`update`](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019) 命令行参数。

## <a name="step-5---optional-use-visual-studio-tools"></a>第 5 步 -（可选）使用 Visual Studio 工具

我们提供了几种工具来帮助你在客户端计算机上[检测和管理安装的 Visual Studio 实例](tools-for-managing-visual-studio-instances.md?view=vs-2019)。

## <a name="advanced-configuration"></a>高级配置

默认情况下，Visual Studio 安装允许从错误列表 F1 和代码链接在必应搜索中包含自定义类型。 可以通过按策略更改以下注册表项的值，将 Visual Studio 配置为禁止搜索机制包括任何自定义用户类型：

**“PutCustomTypeInBingSearch” DWORD 0**

注册表位于专用注册表配置单元的 *Software\Microsoft\VisualStudio\16.0_{InstanceId}\Roslyn\Internal\Diagnostics\* 目录中。 有关如何打开注册表配置单元的说明，请参阅[编辑 Visual Studio 实例的注册表](tools-for-managing-visual-studio-instances.md?view=vs-2019#editing-the-registry-for-a-visual-studio-instance)。

::: moniker-end

::: moniker range="vs-2017"

## <a name="step-1---download-visual-studio-product-files"></a>第 1 步 - 下载 Visual Studio 产品文件

* [选择要安装的工作负载和组件](workload-and-component-ids.md?view=vs-2017)。

* [创建 Visual Studio 产品文件的网络共享](create-a-network-installation-of-visual-studio.md?view=vs-2017)。

## <a name="step-2---build-an-installation-script"></a>第 2 步 - 生成安装脚本

* 生成使用[命令行参数](use-command-line-parameters-to-install-visual-studio.md?view=vs-2017)来控制安装的安装脚本。

  >[!NOTE]
  > 可通过使用[响应文件](automated-installation-with-response-file.md?view=vs-2017)来简化脚本。 确保创建包含默认安装选项的响应文件。

* （可选）[应用批量许可证产品密钥](automatically-apply-product-keys-when-deploying-visual-studio.md?view=vs-2017)作为安装脚本的一部分，这样用户便无需单独激活软件。

* （可选）将网络布局更新为[控制何时何地向最终用户提供产品更新](controlling-updates-to-visual-studio-deployments.md?view=vs-2017)。

* （可选）设置影响 Visual Studio 部署的注册表策略，例如与其他版本或实例共享的一些包的安装位置、[缓存包的位置](set-defaults-for-enterprise-deployments.md?view=vs-2019)或[是否缓存包](disable-or-move-the-package-cache.md?view=vs-2017)。

* （可选）设置组策略。 还可在个人计算机上[将 Visual Studio 配置为禁用客户反馈](../ide/visual-studio-experience-improvement-program.md)。

## <a name="step-3---deploy"></a>第 3 步 - 部署

* 使用所选部署技术，在目标开发者工作站上执行脚本。

## <a name="step-4---deploy-updates"></a>第 4 步 - 部署更新

* 定期运行第 1 步中的命令来添加更新后的组件，使用 Visual Studio [最新更新刷新网络位置](update-a-network-installation-of-visual-studio.md?view=vs-2017)。

  可以使用更新脚本来更新 Visual Studio。 为此，请使用 [`update`](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019) 命令行参数。

## <a name="step-5---optional-use-visual-studio-tools"></a>第 5 步 -（可选）使用 Visual Studio 工具

我们提供了几种工具来帮助你在客户端计算机上[检测和管理安装的 Visual Studio 实例](tools-for-managing-visual-studio-instances.md?view=vs-2017)。

## <a name="advanced-configuration"></a>高级配置

默认情况下，Visual Studio 安装允许从错误列表 F1 和代码链接在必应搜索中包含自定义类型。 可以通过按策略更改以下注册表项的值，将 Visual Studio 配置为禁止搜索机制包括任何自定义用户类型：

**“PutCustomTypeInBingSearch” DWORD 0**

注册表位于专用注册表配置单元的 *Software\Microsoft\VisualStudio\15.0_{InstanceId}\Roslyn\Internal\Diagnostics\* 目录中。 有关如何打开注册表配置单元的说明，请参阅[编辑 Visual Studio 实例的注册表](tools-for-managing-visual-studio-instances.md?view=vs-2017#editing-the-registry-for-a-visual-studio-instance)。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [命令行参数示例](command-line-parameter-examples.md)
* [安装 Visual Studio 脱机安装所需的证书](install-certificates-for-visual-studio-offline.md)
* [导入或导出安装配置](import-export-installation-configurations.md)
* [Visual Studio 安装存档](https://devblogs.microsoft.com/setup/tag/vs2017/)
* [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing/)
* [同步自动加载设置](../extensibility/synchronously-autoloaded-extensions.md)
