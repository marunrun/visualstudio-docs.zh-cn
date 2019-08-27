---
title: 选择 ClickOnce 部署策略 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, strategies
- deploying applications, ClickOnce
ms.assetid: 98bcab65-ab8b-4ed1-9adc-fdacf92b8106
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6b4ed387d00c96c1d66fdac0bb92a0bfbae7c530
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63406677"
---
# <a name="choose-a-clickonce-deployment-strategy"></a>选择 ClickOnce 部署策略
有三种不同的策略用于部署 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序；所选择的策略主要取决于要部署的应用程序的类型。 下面介绍了这三种部署策略：

- 从 Web 或网络共享安装

- 从 CD 安装

- 从 Web 或网络共享启动应用程序

    > [!NOTE]
    > 除了选择部署策略外，您可能还想选择提供应用程序更新的策略。 有关详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

## <a name="install-from-the-web-or-a-network-share"></a>从 Web 或网络共享安装
 在使用此策略时，应用程序会部署到 Web 服务器或网络文件共享。 当最终用户要安装应用程序时，该用户在网页上单击图标或是在文件共享上双击图标。 然后会在最终用户的计算机上下载、安装并启动应用程序。 项被添加到“开始”菜单和“控制面板”中的“添加/删除程序”中。

 因为此策略依赖于网络连接，所以最适合将部署到可以访问局域网或高速 Internet 连接的用户的应用程序。

 如果从 Web 部署应用程序，则可以在使用 URL 激活应用程序时将参数传递给应用程序。 有关详细信息，请参阅[如何：在联机 ClickOnce 应用程序中检索查询字符串信息](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)。 无法将参数传递给使用本文档中描述的任何其他方法激活的应用程序。

 若要在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中启用此部署策略，请在发布向导的“安装方式”页上单击“从 Web”或“从 UNC 路径或文件共享”。

 这是默认部署策略。

## <a name="start-the-application-from-the-web-or-a-network-share"></a>从 Web 或网络共享启动应用程序
 此策略与第一种策略相似，只是应用程序在此策略中的行为类似于 Web 应用程序。 当用户在网页上单击链接（或在文件共享上双击图标）时，应用程序被启动。 当用户关闭应用程序时，应用程序在用户的本地计算机上不再可用；此策略不会向“开始”菜单或“控制面板”中的“添加或删除程序”添加任何内容。

> [!NOTE]
> 从技术角度看，应用程序被下载和安装到本地计算机上的应用程序缓存中，就如同 Web 应用程序被下载到 Web 缓存中一样。 与 Web 缓存一样，最后会从应用程序缓存中清理文件。 但是，从用户的角度来看，应用程序是从 Web 或文件共享运行的。

 此策略最适用于不常用的应用程序，例如，通常一年才运行一次的雇员福利计算工具。

 若要在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中启用此部署策略，请在发布向导的“从 Web 安装或运行”页上单击“不安装应用程序”。

 若要手动启用此部署策略，请更改部署清单中的“install”标记。 （其值可以是“true”或“false”。 在 Mage.exe 中，使用“应用程序类型”列表中的“仅限联机状态”选项。）

## <a name="install-from-a-cd"></a>从 CD 安装
 在使用此策略时，应用程序会部署到可移动媒体（如 CD-ROM 或 DVD）。 与前一种策略一样，当用户选择安装应用程序时，将安装并启动应用程序，并在“开始”菜单和“控制面板”中的“添加/删除程序”中添加项。

 此策略最适合将应用程序部署到不具有持久网络连接或只具有低带宽连接的用户。 因为应用程序是从可移动媒体安装的，所以安装不需要任何网络连接；但是，应用程序更新仍需要网络连接。

 若要在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中启用此部署策略，请在发布向导的“安装方式”页上单击“从 CD-ROM 或 DVD-ROM”。

 若要手动启用此部署策略，请更改部署清单中的“deploymentProvider”标记。 （在 Visual Studio 中，此属性公开为项目设计器“发布”页上的“安装 URL”。 在 Mage.exe 中，它是“启动位置”。）

## <a name="web-browser-support"></a>Web 浏览器支持
 可以使用任何浏览器安装面向 .NET Framework 3.5 的应用程序。

 面向 .NET Framework 2.0 的应用程序需要 Internet Explorer。

## <a name="see-also"></a>请参阅
- [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)