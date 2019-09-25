---
title: 创建用于其他部署的 ClickOnce 应用程序 |Microsoft Docs
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
ms.openlocfilehash: 3307fc124f50e8c9f73749293c36f53be36c5e3c
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71252450"
---
# <a name="create-clickonce-applications-for-others-to-deploy"></a>创建供其他人部署的 ClickOnce 应用程序
并非所有正在创建 ClickOnce 部署的开发人员都计划自行部署应用程序。 其中的许多用户只需使用 ClickOnce 打包应用程序，然后将文件提交给客户（例如大型公司）。 客户成为负责在其网络上托管应用程序的客户。 本主题讨论版本3.5 之前的 .NET Framework 版本中的此类部署所固有的一些问题。 然后，它介绍了在 .NET Framework 3.5 中使用新的 "使用者信任清单" 功能提供的新解决方案。 最后，它使用推荐的策略来为仍使用旧版本 .NET Framework 的客户创建 ClickOnce 部署。

## <a name="issues-involved-in-creating-deployments-for-customers"></a>为客户创建部署所涉及的问题
 当你计划向客户提供部署时，会发生几个问题。 第一个问题涉及到代码签名。 若要通过网络进行部署，ClickOnce 部署的部署清单和应用程序清单必须使用数字证书进行签名。 这样就可以在对清单进行签名时使用开发人员的证书或客户的证书。

 要使用的证书的问题至关重要，因为 ClickOnce 应用程序的标识基于部署清单的数字签名。 如果开发人员签署部署清单，如果客户是一家大型公司，并且公司的多个部门部署了自定义版本的应用程序，则可能会导致冲突。

 例如，艾德公司有一个财务部门和一个人力资源部门。 这两个部门向 Microsoft Corporation 的 ClickOnce 应用程序授予从存储在 SQL 数据库中的数据生成报表的许可。 Microsoft 将为每个部门提供针对其数据自定义的应用程序版本。 如果使用相同的 Authenticode 证书对应用程序进行签名，则尝试使用这两个应用程序的用户会遇到错误，因为 ClickOnce 会将第二个应用程序视为与第一个相同。 在这种情况下，客户可能会遇到不可预知和不需要的副作用，其中包括应用程序在本地存储的任何数据丢失。

 与代码签名相关的另一个问题是`deploymentProvider`部署清单中的元素，该元素告诉 ClickOnce 在哪里查找应用程序更新。 必须先将此元素添加到部署清单，然后才能对其进行签名。 如果以后添加此元素，则必须对部署清单进行重新签名。

### <a name="require-the-customer-to-sign-the-deployment-manifest"></a>要求客户对部署清单进行签名
 针对非唯一部署的此问题的一种解决方案是让开发人员对应用程序清单进行签名，并对部署清单进行签名。 尽管此方法有效，但会引入其他问题。 由于 Authenticode 证书必须保留受保护的资产，因此客户不能只是向开发人员授予证书来对部署进行签名。 尽管客户可以使用 .NET Framework SDK 中免费提供的工具对部署清单进行签名，但这可能需要比客户更愿意或无法提供的技术知识。 在这种情况下，开发人员通常会创建一个应用程序、网站或其他机制，通过该机制，客户可以提交其应用程序版本以进行签名。

### <a name="the-impact-of-customer-signing-on-clickonce-application-security"></a>客户签名对 ClickOnce 应用程序安全的影响
 即使开发人员和客户同意客户应该对应用程序清单进行签名，这也会引发应用程序标识以外的其他问题，特别是应用于受信任的应用程序部署时。 （有关此功能的详细信息，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。）假设艾德公司想要配置其客户端计算机，以便 Microsoft Corporation 向其提供的任何应用程序都以完全信任的方式运行。 如果艾德作品对部署清单进行签名，则 ClickOnce 将使用艾德公司的安全签名来确定应用程序的信任级别。

## <a name="create-customer-deployments-by-using-application-manifest-for-trust"></a>使用应用程序清单进行信任创建客户部署
 .NET Framework 3.5 中的 ClickOnce 包含一项新功能，使开发人员和客户可以通过一个新的解决方案来应对清单的签名方式。 ClickOnce 应用程序清单支持名为`<useManifestForTrust>`的新元素，使开发人员能够表示应用程序清单的数字签名应该用于做出信任决策。 开发人员使用 ClickOnce 打包工具（如*mage.exe*、 *Mageui.exe*和 Visual Studio）将此元素包括在应用程序清单中，以及将其发布者名称和应用程序名称嵌入到清单中。

 使用`<useManifestForTrust>`时，部署清单不必使用证书颁发机构颁发的 Authenticode 证书进行签名。 相反，可以使用所谓的自签名证书对其进行签名。 自签名证书是由客户或开发人员通过使用标准 .NET Framework SDK 工具生成的，然后使用标准 ClickOnce 部署工具应用于部署清单。 有关详细信息，请参阅[MakeCert](/windows/desktop/SecCrypto/makecert)。

 使用部署清单的自签名证书具有几个优点。 通过使客户无需获得或创建自己的 Authenticode 证书， `<useManifestForTrust>`简化了客户的部署，同时允许开发人员在应用程序上维护自己的品牌标识。 结果是一组更安全且具有唯一应用程序标识的已签名部署。 这消除了将同一应用程序部署到多个客户时可能出现的潜在冲突。

 有关如何创建启用了的`<useManifestForTrust>` ClickOnce 部署的分步信息，请参阅[演练：手动部署不需要重新签名并且保留署名信息](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)的 ClickOnce 应用程序。

### <a name="how-application-manifest-for-trust-works-at-run-time"></a>应用程序清单信任在运行时的工作原理
 若要更好地了解如何在运行时使用应用程序清单进行信任，请参阅以下示例。 面向 .NET Framework 3.5 的 ClickOnce 应用程序是由 Microsoft 创建的。 应用程序清单使用`<useManifestForTrust>`元素并由 Microsoft 签名。 艾德作品使用自签名证书对部署清单进行签名。 艾德公司客户端配置为信任由 Microsoft 签署的任何应用程序。

 当用户单击部署清单的链接时，ClickOnce 会在用户的计算机上安装该应用程序。 证书和部署信息在客户端计算机上将应用程序唯一识别为 ClickOnce。 如果用户尝试从不同的位置再次安装同一应用程序，则 ClickOnce 可以使用此标识来确定客户端上已存在该应用程序。

 接下来，ClickOnce 检查用于对应用程序清单进行签名的 Authenticode 证书，该证书确定 ClickOnce 将授予的信任级别。 由于艾德公司已将客户端配置为信任由 Microsoft 签署的任何应用程序，因此此 ClickOnce 应用程序被授予完全信任。 有关详细信息，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

## <a name="create-customer-deployments-for-earlier-versions"></a>为早期版本创建客户部署
 如果开发人员将 ClickOnce 应用程序部署到使用较旧版本的 .NET Framework 的客户怎么办？ 以下各节汇总了几种建议的解决方案，以及每种解决方案的优点和缺点。

### <a name="sign-deployments-on-behalf-of-customer"></a>代表客户对部署进行签名
 一种可能的部署策略是，开发人员通过使用客户自己的私钥创建一种机制，用于代表客户对部署进行签名。 这可以防止开发人员管理私钥或多个部署包。 开发人员只为每个客户提供相同的部署。 由客户使用签名服务对其环境进行自定义。

 此方法的一个缺点是实现该方法所需的时间和费用。 虽然此类服务可以通过使用 .NET Framework SDK 中提供的工具来生成，但它会将更多的开发时间添加到产品生命周期。

 如本主题前面所述，另一个缺点是每个客户的应用程序版本将具有相同的应用程序标识，这可能会导致冲突。 如果这是一个问题，开发人员可以更改生成部署清单时使用的 "名称" 字段，以便为每个应用程序指定唯一名称。 这会为应用程序的每个版本创建一个单独的标识，并消除任何潜在的标识冲突。 此字段对应于 mage.exe `-Name`的参数，并对应于 mageui.exe 中 "**名称**" 选项卡上的 "**名称**" 字段。

 例如，开发人员创建了一个名为 Application1 的应用程序。 开发人员可以创建具有此名称的特定于客户的变体的多个部署，如 Application1-客户较少、Application1-拥有等，而不是创建一个名称字段设置为 Application1 的部署。

### <a name="deploy-using-a-setup-package"></a>使用安装包进行部署
 另一种可能的部署策略是生成 Microsoft 安装项目以执行 ClickOnce 应用程序的初始部署。 这可以采用多种不同的格式之一提供：作为 MSI 部署，作为安装程序可执行文件（。EXE），或作为 cabinet （.cab）文件与批处理脚本一起使用。

 使用此方法，开发人员可以向客户提供一个部署，其中包含应用程序文件、应用程序清单和用作模板的部署清单。 客户将运行安装程序，该程序会提示他们提供部署 URL （用户将在其中安装 ClickOnce 应用程序的服务器或文件共享位置）以及数字证书。 安装应用程序还可以选择提示其他 ClickOnce 配置选项，如更新检查时间间隔。 收集此信息后，安装程序会生成真实的部署清单，对其进行签名，然后将 ClickOnce 应用程序发布到指定的服务器位置。

 在这种情况下，客户可以通过三种方式对部署清单进行签名：

1. 客户可以使用证书颁发机构（CA）颁发的有效证书。

2. 作为此方法的一种变化形式，客户可以选择使用自签名证书对其部署清单进行签名。 这种方法的缺点是，如果询问用户是否安装，将导致应用程序显示 "未知发布者" 字样。 但优点在于，它可以防止较小的客户花费时间和金钱来满足证书颁发机构颁发的证书所需的时间和金钱。

3. 最后，开发人员可以在安装包中包含自己的自签名证书。 这会引入本主题前面所述的应用程序标识的潜在问题。

   安装部署项目方法的缺点是构建自定义部署应用程序所需的时间和费用。

### <a name="have-customer-generate-deployment-manifest"></a>让客户生成部署清单
 第三种可能的部署策略是仅将应用程序文件和应用程序清单交付给客户。 在此方案中，客户负责使用 .NET Framework SDK 生成并签署部署清单。

 此方法的缺点是要求客户安装 .NET Framework SDK 工具，并让开发人员或系统管理员熟练使用这些工具。 有些客户可能需要对其部分进行少量或不需要技术工作的解决方案。

## <a name="see-also"></a>请参阅
- [部署用于测试和生产服务器的 ClickOnce 应用程序而无需让步](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)
- [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [演练：手动部署不需要重新签名且保留品牌信息的 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)