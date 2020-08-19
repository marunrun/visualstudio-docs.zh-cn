---
title: Visual Studio Enterprise 指南
description: 在企业环境中安装 Visual Studio 并对其进行故障排除。
ms.date: 07/29/2020
ms.custom: seodec18
ms.topic: overview
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
ms.assetid: ''
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 02ce09aebae0d6e5225ba1cdfa7484aa887135fd
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88247638"
---
# <a name="visual-studio-enterprise-guide"></a>Visual Studio Enterprise 指南
如果你想节省在 Visual Studio 上正常运行公司业务的时间，请阅读本文。 本企业指南提供了一些提示，可帮助你在常见的企业场景中安装和更新 Visual Studio、在遇到问题时解决问题，并了解如何在需要更多帮助的情况下报告问题。 

## <a name="get-started"></a>入门 
了解如何在联网和脱机环境中将 Visual Studio 部署到企业。 

- **了解联网环境中的企业部署选项**。 [Visual Studio 管理员指南](visual-studio-administrator-guide.md)为系统管理员提供基于应用场景的指南。 

- **[获取故障排除提示](troubleshooting-installation-issues.md)** 。 在安装或更新 Visual Studio 时获得帮助，并了解在遇到问题时如何报告问题。 这些提示包含可解决大多数联机或脱机安装问题的分步说明。 

- **[创建 Visual Studio 的脱机安装](create-an-offline-installation-of-visual-studio.md)** 。 如果未连接到 Internet 或 Internet 连接受限，可以找到用于安装 Visual Studio 的选项。 

- **[创建引导程序包](../deployment/creating-bootstrapper-packages.md)** 。 了解如何通过创建产品和包清单来创建自定义引导程序包。 

- **[在部署 Visual Studio 时自动应用产品密钥](automatically-apply-product-keys-when-deploying-visual-studio.md)** 。 可采用编程方式将产品密钥作为用于自动化 Visual Studio 部署的脚本的一部分进行应用。 安装 Visual Studio 期间或安装已完成后，可采用编程方式在设备上设置产品密钥。 

## <a name="install-visual-studio"></a>安装 Visual Studio 

了解如何在常见的企业应用场景中安装 Visual Studio。 

- **[使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)** 。 使用各种参数来控制或自定义 Visual Studio 安装。 自动执行安装过程，或创建安装文件的缓存供以后使用。 

- **参阅 [Visual Studio 安装命令行参数示例](command-line-parameter-examples.md)** 。 为了说明如何使用命令行参数来安装 Visual Studio，请查看多个示例，你可以根据自己的需求自定义这些示例。 

- **[在防火墙或代理服务器后面安装和使用 Visual Studio 和 Azure 服务](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)** 。 如果你的组织使用防火墙或代理服务器等安全措施，则包含有可能需要将其添加到“允许列表”的域 URL，以及可能需要打开的端口和协议，以便在安装和使用 Visual Studio 以及 Azure 服务时获得最佳体验。 

- **[创建 Visual Studio 的网络安装](create-a-network-installation-of-visual-studio.md)** . 将初始安装的相关文件以及所有产品更新缓存到一个文件夹中。  

## <a name="update-visual-studio"></a>更新 Visual Studio 

了解如何成功更新 Visual Studio 并修复更新问题。 

- **[更新基于网络的 Visual Studio 安装](update-a-network-installation-of-visual-studio.md)** 。 使用最新的产品更新来更新 Visual Studio 的网络安装布局，以便将它用作 Visual Studio 最新更新的安装点，同时还可用于维护已部署到客户端工作站的安装。

- **[在维修基线上更新 Visual Studio](update-servicing-baseline.md)** 。 了解更新基线的重要性，并了解次要版本与服务更新之间的差异。 

- **[使用最小脱机布局更新 Visual Studio](update-minimal-layout.md)** 。 对于未连接到 Internet 的计算机，创建最小布局是更新脱机 Visual Studio 实例的最简单、最快捷的方法。

- **[修复 Visual Studio](repair-visual-studio.md) 以解决更新问题**。 Visual Studio 安装有时会损毁或损坏。 修复对于修复所有安装操作（包括更新）中的安装时问题非常有用。 

- **按照** [Windows 安全基线](https://docs.microsoft.com/windows/security/threat-protection/windows-security-baselines)的说明操作。 Microsoft 专注于为客户提供安全的操作系统（如 Windows 10 和 Windows Server）以及安全的应用（如 Microsoft Edge）。 除了产品的安全保障，Microsoft 还通过提供各种配置功能使你良好地控制环境。 

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅 

- [Visual Studio 实用指南](../ide/productivity-features.md)
