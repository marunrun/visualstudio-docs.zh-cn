---
title: 在维修基线上更新 Visual Studio
description: 了解如何在维修基线上更新 Visual Studio。
ms.date: 07/17/2019
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: ''
author: doughall
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 4e84704d4ca37dd9e36da3838b5b1b23f068568c
ms.sourcegitcommit: 978df2feb5e64228d2e3dd430b299a5c234cda17
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72888580"
---
# <a name="update-visual-studio-while-on-a-servicing-baseline"></a>在维修基线上更新 Visual Studio

我们经常在 Visual Studio 的产品生命周期中更新它。 有两种类型的更新： 

* **次要版本更新** &mdash; 例如从 16.0 更新到 16.1&mdash;，其中包含新功能和组件。  
* **服务更新** - 例如，从 16.0.4 更新到 16.0.5，仅包含针对关键问题的目标修复。

企业管理员可以选择将其客户端保管在维护基线上。 在发布下一个维护基线后的一年内将使用维护更新支持该维护基线。

维护基线选项使开发人员和管理员可以更灵活地采用新功能、bug 修补程序或新次要更新包含的组件。 首个维护基线为 16.0.x。 有关详细信息，请参阅[企业版和专业版客户的支持选项](/visualstudio/releases/2019/servicing#support-options-for-enterprise-and-professional-customers)。

## <a name="how-to-get-onto-a-servicing-baseline"></a>如何访问维护基线

请从下面的网站下载 Visual Studio 安装程序引导程序的不可编辑的版本，以开始使用维护基线：[My.VisualStudio.com](https://my.visualstudio.com/Downloads?q=visual%20studio%202019%20version%2016.0)。 这些引导程序包含产品配置、工作负载和该特定版本组件的链接。

> [!NOTE]
> 请注意区分不可编辑版本的引导程序和标准引导程序。 标准引导程序已配置为使用 Visual Studio 的最新可用版本。 从 My.VisualStudio.com 下载标准引导程序后，它们的文件名包含编号（例如 vs_enterprise__123456789-123456789.exe）。

安装时，企业管理员必须配置自己的客户端，以防止客户端更新到最新版本。 有若干方法可实现此操作：
- [更改响应配置文件中的 `channelUri` 设置](update-servicing-baseline.md#install-a-servicing-baseline-on-a-network)，以在布局或本地文件夹中使用通道清单。
- [通过命令行执行修改 channelUri](update-servicing-baseline.md#install-a-servicing-baseline-via-the-internet)，以使用不存在的文件。
- [在客户端系统上设置策略来禁用更新](update-servicing-baseline.md#use-policy-settings-to-disable-clients-from-updating)，以防止客户端自更新。

### <a name="install-a-servicing-baseline-on-a-network"></a>在网络上安装维护基线

使用网络布局安装的管理员应修改布局中 response.json  文件的 `channelUri` 值，以使用同一个文件夹中的 channelmanifest.json  文件。 有关要执行的步骤，请参阅[控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)。 更改 `channelUri` 后，客户端即可从布局位置查找更新。

### <a name="install-a-servicing-baseline-via-the-internet"></a>通过 Internet 安装维护基线

对于基于 Internet 的安装，请将使用不存在的通道清单的 `--channelUri` 添加到用于启动安装的命令行。 这样 Visual Studio 将无法使用最新可用版本更新。 以下是一个示例：

```cmd
vs_enterprise.exe --channelUri c:\doesnotexist.chman
```

### <a name="use-policy-settings-to-disable-clients-from-updating"></a>使用策略设置阻止客户端更新

此外，还可以选择通过[关闭更新通知](controlling-updates-to-visual-studio-deployments.md)来控制客户端上的更新。 若未在安装过程中更改 channelUri 值，请使用此选项。 这样客户端将无法接收最新可用版本的链接。 若要在客户端上更新到特定版本，仍然需要不可编辑版本的引导程序。

## <a name="how-to-stay-on-a-servicing-baseline"></a>如何访问维护基线

若提供了维护基线更新，[My.VisualStudio.com](https://my.visualstudio.com/Downloads?q=visual%20studio%202019%20version%2016.0) 将向该维护更新提供不可编辑版本的引导程序文件。

对于使用网络布局安装进行部署的管理员，管理员应更新[布局位置](update-a-network-installation-of-visual-studio.md)。 从该位置安装的客户端将收到更新通知。 如果必须将更新部署到客户端，请按照[这些说明](update-a-network-installation-of-visual-studio.md#how-to-deploy-an-update-to-client-machines)操作。 通过修改“response.json”来获取更新时，请不要添加其他工作负载、组件或语言。 更新产品后，必须以“修改”部署的形式管理这些设置。

对于基于 Internet 的安装，请在客户端上使用指向不存在的通道清单的 `--channelUri` 参数运行新的不可编辑版本的引导程序。 若使用安静或被动模式部署更新，请使用下面的两个独立的命令：

1. 更新 Visual Studio 安装程序：

    ```cmd
    vs_enterprise.exe --quiet --update
    ```

2. 更新 Visual Studio 应用程序本身：

    ```cmd
    vs_enterprise.exe update --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" --quiet --wait --norestart --channelUri c:\doesnotexist.chman
    ```

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [用于检测和管理 Visual Studio 实例的工具](tools-for-managing-visual-studio-instances.md)
* [如何在响应文件中定义设置](automated-installation-with-response-file.md)
* [控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)
* [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing/)
