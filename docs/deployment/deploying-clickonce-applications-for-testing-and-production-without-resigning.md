---
title: 无需重新签名即可部署 ClickOnce 应用
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, deploying without resigning
- ClickOnce deployment, without resigning
- application updates, ClickOnce
- update location [ClickOnce]
- deploymentProvider tag
- manifests [ClickOnce]
ms.assetid: 1218a98d-1ad5-4eef-95dd-0e0b3c44168c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 89e1d7970b26d5ba9bd49090362a6a4e8c09f78d
ms.sourcegitcommit: d6828e7422c8d74ec1e99146fedf0a05f757245f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "80395324"
---
# <a name="deploy-clickonce-applications-for-testing-and-production-servers-without-resigning"></a>部署 ClickOnce 应用程序以进行测试和生产服务器，无需重新分配
本文介绍了 .NET Framework 版本 3.5 中引入的 ClickOnce 功能，该功能支持从多个网络位置部署 ClickOnce 应用程序，而无需重新签名或更改 ClickOnce 清单。

> [!NOTE]
> 重新分配仍然是部署新版本应用程序的首选方法。 只要有可能，请使用重新分配方法。 有关详细信息，请参阅[*Mage.exe（* 清单生成和编辑工具）。](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)

 第三方开发人员和 ISV 可以选择加入此功能，从而简化其客户更新其应用程序。 此功能可用于以下情况：

- 更新应用程序时，不是应用程序的第一次安装。

- 当计算机上只有一个应用程序配置时。 例如，如果应用程序配置为指向两个不同的数据库，则无法使用此功能。

## <a name="exclude-deploymentprovider-from-deployment-manifests"></a>从部署清单中排除部署提供程序
 在 .NET 框架 2.0 和 .NET 框架 3.0 中，在系统上安装以进行脱机可用性的任何`deploymentProvider`ClickOnce 应用程序都必须在其部署清单中列出 。 通常`deploymentProvider`称为更新位置;它是 ClickOnce 检查应用程序更新的位置。 这一要求，以及应用程序发布者需要签署其部署，使公司难以更新来自供应商或其他第三方的 ClickOnce 应用程序。 它还使在同一网络上的多个位置部署同一应用程序变得更加困难。

 通过对 .NET 框架 3.5 中的 ClickOnce 所做的更改，第三方可以将 ClickOnce 应用程序提供给另一个组织，然后该组织可以在自己的网络上部署应用程序。

 为了利用此功能，ClickOnce 应用程序的开发人员必须从其部署清单中排除`deploymentProvider`。 此要求意味着，在使用 Mage.exe 创建部署清单时，必须排除`-providerUrl`参数。 或者，如果要使用 MageUI.exe 生成部署清单，则必须确保 **"应用程序清单**"选项卡上的 **"启动位置**"文本框留空。

## <a name="deploymentprovider-and-application-updates"></a>部署提供程序和应用程序更新
 从 .NET 框架 3.5 开始，您不再需要在部署`deploymentProvider`清单中指定 ，即可部署 ClickOnce 应用程序以用于联机和脱机使用。 此更改支持需要自行打包和签名部署，但允许其他公司在其网络上部署应用程序的方案。

 需要记住的要点是，排除 的`deploymentProvider`应用程序在更新期间无法更改其安装位置，直到他们再次发布包含`deploymentProvider`标记的更新。

 下面是两个示例来阐明这一点。 在第一个示例中，您发布一`deploymentProvider`个没有标记的 ClickOnce 应用程序，并要求用户从`http://www.adatum.com/MyApplication/`安装该应用程序。 如果您决定要发布应用程序的`http://subdomain.adatum.com/MyApplication/`下一个更新，则无法在驻留在 的部署清单中`http://www.adatum.com/MyApplication/`表示这一点。 你可以做两件事之一：

- 告诉用户卸载以前的版本，并从新位置安装新版本。

- 包括包含`http://www.adatum.com/MyApplication/``deploymentProvider`指向`http://www.adatum.com/MyApplication/`的更新。 然后，稍后使用`deploymentProvider`指向`http://subdomain.adatum.com/MyApplication/`发布另一个更新。

  在第二个示例中，您发布指定`deploymentProvider`的 ClickOnce 应用程序，然后决定删除它。 将没有新版本`deploymentProvider`下载到客户端后，在发布已`deploymentProvider`还原的应用程序版本之前，无法重定向用于更新的路径。 与第一个示例一`deploymentProvider`样，必须最初指向当前更新位置，而不是新位置。 在这种情况下，如果尝试插入引用`deploymentProvider``http://subdomain.adatum.com/MyApplication/`的 ，则下一次更新将失败。

## <a name="create-a-deployment"></a>创建部署
 有关创建可以从不同网络位置部署的部署的分步指南，请参阅[演练：手动部署不需要重新签名并保留品牌信息的 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)。

## <a name="see-also"></a>请参阅
- [*Mage.exe（* 清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [*MageUI.exe（* 清单生成和编辑工具，图形客户端）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
