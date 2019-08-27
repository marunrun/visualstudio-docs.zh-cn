---
title: 访问 ClickOnce 应用程序中的本地和远程数据 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, data
- data access, ClickOnce applications
ms.assetid: be5cbe12-6cb6-49c9-aa59-a1624e1eef3d
caps.latest.revision: 23
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1ce6b6ee633e926709b0c15c2234077055600a07
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65688120"
---
# <a name="accessing-local-and-remote-data-in-clickonce-applications"></a>在 ClickOnce 应用程序中访问本地数据和远程数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

大多数应用程序使用或生成数据。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 为你提供多种选项用于在本地及远程读取和写入数据。  
  
## <a name="local-data"></a>本地数据  
 借助 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]，你可以通过以下任意一种方法在本地加载和存储数据：  
  
- [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 数据目录  
  
- 独立存储  
  
- 其他本地文件  
  
### <a name="clickonce-data-directory"></a>ClickOnce 数据目录  
 本地计算机上安装的每个 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序都有一个数据目录，该数据目录存储在用户的 Documents and Settings 文件夹中。 安装应用程序时，会将 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序中包含的且标记为“数据”文件的所有文件复制到此目录。 数据文件可以是任何类型的文件，最常用的是文本文件、XML 文件和数据库文件（如 Microsoft Access.mdb 文件）。  
  
 数据目录预期用于应用程序管理的数据，即应用程序显式存储和维护的数据。 应用程序清单中未标记为“数据”的所有静态非依赖文件都将改为驻留在应用程序目录中。 此目录是应用程序的可执行文件 (.exe) 文件和程序集所在的位置。  
  
> [!NOTE]
> 卸载 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序时，也会删除其数据目录。 切勿使用数据目录来存储最终用户管理的数据，如文档。  
  
#### <a name="marking-data-files-in-a-clickonce-distribution"></a>在 ClickOnce 分发中标记数据文件  
 若要将现有文件放入数据目录，必须在 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序的应用程序清单文件中将现有文件标记为数据文件。 有关详细信息，请参阅[如何：将数据文件添加到 ClickOnce 应用程序中](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md)。  
  
#### <a name="reading-from-and-writing-to-the-data-directory"></a>读取和写入数据目录  
 读取数据目录要求你的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序请求读取权限；同样，写入目录也需要写入权限。 如果它被配置为使用完全信任的权限运行，则你的应用程序将自动拥有此权限。 有关提升权限的使用权限提升或受信任的应用程序部署的应用程序的详细信息，请参阅[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。  
  
> [!NOTE]
> 如果你的组织不使用信任的应用程序部署，并且已经关闭了权限提升，则断言权限将失效。  
  
 应用程序具有这些权限后，就可以通过对 <xref:System.IO>中的类进行方法调用访问数据目录。 你可以通过使用在 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 的 <xref:System.Deployment.Application.ApplicationDeployment.DataDirectory%2A> 属性上定义的 <xref:System.Deployment.Application.ApplicationDeployment.CurrentDeployment%2A> 属性，获取 Windows 窗体 <xref:System.Deployment.Application.ApplicationDeployment>应用程序中数据目录的路径。 这是访问数据的最简便方法，并且推荐使用此方法。 下面的代码示例演示如何对名为 CSV.txt 且已作为数据文件包括到部署中的文本文件执行此操作。  
  
 [!code-csharp[ClickOnce.OpenDataFile#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnce.OpenDataFile/CS/Form1.cs#1)]
 [!code-vb[ClickOnce.OpenDataFile#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnce.OpenDataFile/VB/Form1.vb#1)]  
  
 将标记为数据文件在部署中的文件的详细信息，请参阅[如何：将数据文件添加到 ClickOnce 应用程序中](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md)。  
  
 你还可以使用 <xref:System.Windows.Forms.Application> 类上的相关变量（如 <xref:System.Windows.Forms.Application.LocalUserAppDataPath%2A>）来获取数据目录路径。  
  
 处理其他类型的文件可能需要其他权限。 例如，如果希望使用 Access 数据库 (.mdb) 文件，你的应用程序必须声明完全信任才能使用相关的 <xref:System.Data> 类。  
  
#### <a name="data-directory-and-application-versions"></a>数据目录和应用程序版本  
 应用程序的每个版本都具有其自己的数据目录，每个版本的数据目录相互独立。 无论数据文件是否包括到部署中，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 都将创建此目录，以便该应用程序在运行时有一个位置可以创建新的数据文件。 安装新的应用程序版本时， [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 会将现有全部数据文件从以前版本的数据目录复制到新版本的数据目录，而无论这些数据文件是原始部署中包括的还是应用程序创建的数据文件。  
  
 如果旧版应用程序中的数据文件与新版应用程序具有不同的哈希值，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 会将旧版文件替换为新版服务器。 此外，如果旧版应用程序创建的新文件与新版部署中包括的文件具有相同的名称， [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 会将旧版文件覆盖为新文件。 在这两种情况下，旧文件都将包括到名为 `.pre`的数据目录内部的子目录下，以便应用程序仍然可以访问旧数据以进行迁移。  
  
 如果需要更细粒度的数据迁移，则可以使用 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署 API 执行从旧数据目录到新数据目录的自定义迁移。 你必须使用 <xref:System.Deployment.Application.ApplicationDeployment.IsFirstRun%2A>测试是否可以下载，使用 <xref:System.Deployment.Application.ApplicationDeployment.Update%2A> 或 <xref:System.Deployment.Application.ApplicationDeployment.UpdateAsync%2A>下载更新，以及在更新完成后用自己的方式进行任何自定义数据迁移工作。  
  
### <a name="isolated-storage"></a>独立存储  
 独立存储提供一个 API，用于通过一个简单的 API 创建和访问文件。 存储文件的实际位置对开发人员和用户来说都是隐藏的。  
  
 独立存储适用于 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]的所有版本。 独立存储也适用于部分信任的应用程序，而无需授予其他权限。 如果你的应用程序必须在部分信任环境中运行，但必须维护应用程序特定的数据，则应使用独立存储。  
  
 有关详细信息，请参阅 [独立存储](https://msdn.microsoft.com/library/aff939d7-9e49-46f2-a8cd-938d3020e94e)。  
  
### <a name="other-local-files"></a>其他本地文件  
 如果你的应用程序必须处理或保存最终用户数据（例如报表、图像、音乐等），你的应用程序将需要 <xref:System.Security.Permissions.FileIOPermission> 来读取本地文件系统中的数据以及将数据写入本地文件系统。  
  
## <a name="remote-data"></a>远程数据  
 在某些时候，你的应用程序可能需要从远程网站检索信息（如客户数据或市场信息）。 本部分讨论用于检索远程数据的最常用技术。  
  
### <a name="accessing-files-by-using-http"></a>通过使用 HTTP 访问文件  
 你可以通过使用 <xref:System.Net.WebClient> 命名空间中的 <xref:System.Net.HttpWebRequest> 或 <xref:System.Net> 类从 Web 服务器访问数据。 数据可以是静态文件，也可以是运行原始文本或 XML 数据的 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 应用程序。 如果你的数据为 XML 格式，则检索数据最快的方法是使用 <xref:System.Xml.XmlDocument> 类，该类的 <xref:System.Xml.XmlDocument.Load%2A> 方法采用 URL 作为参数。 有关示例，请参见 [Reading an XML Document into the DOM](https://msdn.microsoft.com/library/a4fb291f-5630-49ba-a49a-5b66c3b71e49)。  
  
 当应用程序通过 HTTP 访问远程数据时，你需要考虑安全性。 默认情况下， [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序对网络资源的访问可能受限，具体取决于应用程序的部署方式。 应用这些限制的目的是防止恶意程序获得对特权远程数据的访问或利用用户的计算机攻击网络上的其他计算机。  
  
 下表列出了可能使用的部署策略及其默认 Web 权限。  
  
|部署类型|默认网络权限|  
|---------------------|---------------------------------|  
|Web 安装|只能从安装应用程序的 Web 服务器访问|  
|文件共享安装|不能访问任何 Web 服务器|  
|CD-ROM 安装|不能访问任何 Web 服务器|  
  
 如果你的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序因安全限制而不能访问 Web 服务器，则应用程序必须为该网站断言 <xref:System.Net.WebPermission> 。 有关增加的安全权限的详细信息[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序，请参阅[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。  
  
### <a name="accessing-data-through-an-xml-web-service"></a>通过 XML Web 服务访问数据  
 如果以 XML Web 服务形式公开你的数据，则可以通过使用 XML Web 服务代理来访问数据。 代理是你使用 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 创建的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]类。 XML Web 服务的操作（如检索客户、下订单等）在代理中作为方法公开。 这使得 Web 服务相比原始文本和 XML 文件更易于使用。  
  
 如果你的 XML Web 服务通过 HTTP 操作，该服务将与 <xref:System.Net.WebClient> 和 <xref:System.Net.HttpWebRequest> 类受到相同的安全限制约束。  
  
### <a name="accessing-a-database-directly"></a>直接访问数据库  
 你可以使用 <xref:System.Data> 命名空间中的类来与网络上的数据库服务器（如 SQL Server）建立直接联系，但必须考虑安全问题。 与 HTTP 请求不同，在部分信任的环境下，数据库连接请求始终默认处于禁止状态；仅当你从 CD-ROM 安装 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序，才默认具有此类权限。 这样，你的应用程序即具有完全信任的权限。 若要实现对特定 SQL Server 数据库的访问，你的应用程序必须向其请求 <xref:System.Data.SqlClient.SqlClientPermission> ；若要实现对 SQL Server 以外的数据库的访问，必须请求 <xref:System.Data.OleDb.OleDbPermission>。  
  
 大多数情况下，你将不必直接访问数据，但将改为通过写入 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 的 Web 服务器应用程序或 XML Web 服务访问。 如果你的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序是从 Web 服务器部署的，则以这种方式访问数据库通常是最好的方法。 你可以使用部分信任的权限访问服务器，而无需提升你的应用程序权限。  
  
## <a name="see-also"></a>请参阅  
 [如何：将数据文件添加到 ClickOnce 应用程序中](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md)
