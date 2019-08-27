---
title: 创建 ClickOnce 供其他应用程序部署 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- preserved branding information
- useManifestForTrust element
- customer deployments [ClickOnce]
- multiple ClickOnce deployment and branding
- ClickOnce applications, previous .NET Framework versions
- application manifests [ClickOnce]
- <useManifestForTrust> element
- manifests [ClickOnce]
- trust applications, ClickOnce
- ClickOnce applications, deployed by others
- ClickOnce applications, previous .NET Framework
ms.assetid: d20766c7-4ef3-45ab-8aa0-3f15b61eccaa
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 01e85c0257d372fa9b27ec5f031aae61132f7edc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62928913"
---
# <a name="create-clickonce-applications-for-others-to-deploy"></a>创建供其他人部署的 ClickOnce 应用程序
并非所有开发人员正在创建 ClickOnce 部署都计划来部署应用程序本身。 其中许多只需将其应用程序打包使用 ClickOnce，然后将文件提交给客户，如大公司。 客户将成为一个负责承载其网络上的应用程序。 本主题讨论了一些在 3.5 版之前的.NET Framework 的版本中的此类部署中固有的问题。 然后，它介绍通过使用新的"使用信任的清单"功能在.NET Framework 3.5 中提供的一个新的解决方案。 最后，则可以确定创建的客户仍在使用较旧版本的.NET Framework 的 ClickOnce 部署的建议策略。

## <a name="issues-involved-in-creating-deployments-for-customers"></a>在为客户创建部署时所涉及的问题
 当你计划提供给客户的部署时，会出现几个问题。 第一个问题涉及代码签名。 为了能够通过网络部署，部署清单和 ClickOnce 部署的应用程序清单必须同时使用数字证书进行签名。 这就提高了这个问题时是否使用开发人员证书或客户的证书对清单进行签名。

 要使用的证书问题非常严重，因为 ClickOnce 应用程序的标识基于部署清单的数字签名。 如果开发人员对部署清单进行签名，它可能导致冲突，如果客户是一家大型公司，并且多个部门的公司将部署应用程序的自定义的版本。

 例如，假设 Adventure Works 具有财务部门和人力资源部门。 这两个部门许可证 SQL 数据库中存储的数据生成报告的 Microsoft Corporation 的 ClickOnce 应用的程序。 Microsoft 提供了每个部门为其数据自定义应用程序的版本。 如果使用相同的验证码证书进行签名的应用程序，尝试使用这两个应用程序的用户会遇到错误，因为 ClickOnce 会认为第二个应用程序作为第一个相同。 在这种情况下，客户可能会出现不可预知和不需要的负面影响，包括应用程序在本地存储的任何数据丢失。

 其他问题的相关代码签名是`deploymentProvider`告诉 ClickOnce 在哪里查找应用程序更新的部署清单中的元素。 此元素必须添加到部署清单之前对它的签名。 如果之后添加此元素，则必须重新签名部署清单。

### <a name="require-the-customer-to-sign-the-deployment-manifest"></a>要求客户部署清单进行签名
 这一问题的非唯一的部署的一种解决方案是让开发人员登录应用程序清单和客户对部署清单进行签名。 尽管这种方法有效，它引入了其他问题。 验证码证书必须保留受保护的资产，由于客户不能为开发人员对签名部署只需指定证书。 虽然客户可以部署对清单进行签名本身通过使用免费提供的工具和.NET Framework SDK，这可能需要超过客户愿意或能够提供更多技术知识。 在这种情况下，开发人员通常会创建应用程序、 Web 站点或其他机制，通过该客户可以提交其版本进行签名的应用程序。

### <a name="the-impact-of-customer-signing-on-clickonce-application-security"></a>在 ClickOnce 应用程序安全登录的客户的影响
 即使开发人员和客户同意客户应该对应用程序清单进行签名，这会引发其他问题，应用程序的标识，尤其是当其应用到受信任的应用程序部署。 (有关此功能的详细信息，请参阅[受信任应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。)假设 Adventure Works 想要配置其客户端计算机，以便由 Microsoft Corporation 提供给他们的任何应用程序以完全信任方式运行。 如果 Adventure Works 对部署清单进行签名，则 ClickOnce 将使用 Adventure Work 安全签名来确定应用程序的信任级别。

## <a name="create-customer-deployments-by-using-application-manifest-for-trust"></a>客户部署使用创建的应用程序清单信任
 ClickOnce 的.NET Framework 3.5 中包含一项新功能，让开发人员和客户的新解决方案对方案进行签名的清单的方式。 ClickOnce 应用程序清单支持名为的新元素`<useManifestForTrust>`，使开发人员来表示的数字签名的应用程序清单是应使用来做出信任决定。 开发人员可以使用 ClickOnce 打包工具，如*Mage.exe*， *MageUI.exe*，和 Visual Studio-若要在应用程序清单中包含此元素，以及要嵌入这两个发布服务器名称和在清单中的应用程序的名称。

 当使用`<useManifestForTrust>`，部署清单不需要使用由证书颁发机构颁发的验证码证书进行签名。 相反，它可以使用所谓的自签名证书进行签名。 自签名的证书是由客户或开发人员通过使用标准的.NET Framework SDK 工具生成，然后使用标准的 ClickOnce 部署工具部署清单中应用。 有关详细信息，请参阅[MakeCert](/windows/desktop/SecCrypto/makecert)。

 使用自签名的证书进行部署清单提供了几个优势。 通过消除对客户可获取或创建自己的验证码证书，需要`<useManifestForTrust>`简化了部署，客户，同时还允许开发人员维护他们自己的应用程序上的品牌标识。 结果是更安全，并且具有唯一的应用程序标识的已签名部署一组。 这消除了从相同应用程序部署到多个客户可能会发生潜在冲突。

 有关如何创建使用 ClickOnce 部署的分步信息`<useManifestForTrust>`启用，请参阅[演练：手动部署 ClickOnce 应用程序，不需要重新签名并且保留署名信息](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)。

### <a name="how-application-manifest-for-trust-works-at-runtime"></a>在运行时的信任的应用程序清单工作原理
 若要获取使用信任的应用程序清单在运行时的工作方式更好地理解，请考虑下面的示例。 面向.NET Framework 3.5 的 ClickOnce 应用程序是由 Microsoft 创建的。 应用程序清单使用`<useManifestForTrust>`元素和由 Microsoft 签名。 Adventure Works 通过使用自签名的证书对签名部署清单。 Adventure Works 客户端配置为信任由 Microsoft 签名的任何应用程序。

 当用户单击部署清单的链接时，ClickOnce 会在用户计算机上安装应用程序。 该证书和部署信息标识唯一地向客户端计算机上的 ClickOnce 应用程序。 如果用户尝试从不同位置重新安装同一应用程序，ClickOnce 可以使用此标识来确定应用程序已存在的客户端上。

 接下来，ClickOnce 会检查用于签署确定 ClickOnce 将授予的信任级别的应用程序清单的 Authenticode 证书。 Adventure Works 已配置为信任由 Microsoft 签名的任何应用程序及其客户端，因为此 ClickOnce 应用程序被授予完全信任。 有关详细信息，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

## <a name="create-customer-deployments-for-earlier-versions"></a>创建客户部署的早期版本
 如果开发人员是 ClickOnce 应用程序部署到使用较旧版本的.NET Framework 的客户？ 以下部分汇总了几个建议的解决方案，以及每个的优缺点。

### <a name="sign-deployments-on-behalf-of-customer"></a>代表客户登录部署
 一种可能的部署策略是为开发人员创建一种机制来使用客户自己的私钥签名代表其客户的部署。 这会阻止开发人员无需管理私钥，或者多个部署包。 开发人员只需为每个客户提供相同的部署。 它是由客户负责使用签名服务自它定义适合其环境。

 此方法的一个缺点是花费时间和实现其所需的费用。 虽然可以使用.NET Framework SDK 中提供的工具来生成此类服务，它将向产品生命周期内添加更多的开发时间。

 如本主题中前面所述，另一个缺点是每个客户的版本的应用程序将具有相同的应用程序标识，这可能导致冲突。 如果这是一个问题，开发人员可以更改名称字段用于生成部署清单时为每个应用程序提供一个唯一的名称。 这会创建不同的标识，每个版本的应用程序，并消除任何潜在的标识冲突。 此字段对应于`-Name`Mage.exe，以及为参数**名称**字段**名称**MageUI.exe 中的选项卡。

 例如，假设开发人员已创建名为应用程序 1 的应用程序。 而不是使用名称字段设置为应用程序 1 中创建一个部署，开发人员可以使用此名称，例如应用程序 1 CustomerA，Application1-CustomerB 的特定于客户的变体创建多个部署，依此类推。

### <a name="deploy-using-a-setup-package"></a>使用安装包进行部署
 第二个可能的部署策略是生成的 Microsoft 安装程序项目来执行初始部署的 ClickOnce 应用程序。 这可以提供多种不同的格式之一： 作为 MSI 部署，作为安装程序可执行 (。Exe 文件），或作为 cabinet (.cab) 文件以及批处理脚本。

 使用此方法，开发人员会向客户提供的部署，包括应用程序文件、 应用程序清单和用作模板的部署清单。 客户将运行安装程序会提示客户部署 URL （服务器或文件共享的用户将在其中安装 ClickOnce 应用程序的位置） 时，以及数字签名。 在安装应用程序还可以选择提示输入其他 ClickOnce 配置选项，例如更新检查间隔。 此信息收集之后，安装程序会生成实际的部署清单、 其签名，和 ClickOnce 应用程序发布到指定的服务器位置。

 有三种方法，客户可以在此情况下对部署清单进行签名：

1. 客户可以使用由证书颁发机构 (CA) 颁发的有效证书。

2. 作为此方法的变体，客户可以选择使用自签名证书及其部署清单进行签名。 对此的缺点是，它将导致应用程序时将其安装要求用户显示单词"未知发行商"。 但是，好处是它可防止较小的客户无需花费时间和金钱所需的证书颁发机构颁发的证书。

3. 最后，开发人员可以安装包中包含其自己的自签名的证书。 它引入了与本主题前面所述的应用程序标识的潜在问题。

   安装程序部署项目方法的缺点是花费时间和生成自定义部署应用程序所需的费用。

### <a name="have-customer-generate-deployment-manifest"></a>已生成的部署清单的客户
 第三个可能的部署策略是仅应用程序关闭文件和应用程序清单复制到客户。 在此方案中，客户负责使用.NET Framework SDK 来生成和部署清单进行签名。

 此方法的缺点是，它需要安装.NET Framework SDK 工具，并使开发人员或系统管理员是擅长使用其客户。 某些客户可能需要一种解决方案，需要在很少或没有技术工作。

## <a name="see-also"></a>请参阅
- [无需重新签名部署 ClickOnce 应用程序测试和生产服务器](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)
- [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [演练：手动部署不需要重新签名且保留品牌信息的 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)