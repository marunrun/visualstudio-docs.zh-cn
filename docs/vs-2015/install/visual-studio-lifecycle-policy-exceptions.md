---
title: Visual Studio 生命周期策略异常 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
ms.assetid: c238489d-6181-42c6-aa60-f75d0889dc68
caps.latest.revision: 3
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: b17693523c75dc434fdda258c07a9b17ecfda1b0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180235"
---
# <a name="visual-studio-lifecycle-policy-exceptions"></a>Visual Studio 生命周期策略异常
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 包含能够在多个 Microsoft 平台进行开发的编译器、语言、运行时、环境和其他资源的集合。 为方便我们的 Visual Studio 客户，Visual Studio 可能会安装某些 Microsoft SDK 以及面向和支持这些 Microsoft 平台的其他 Microsoft 组件。 这些组件根据其自身的条款和政策被授予许可并受到支持。  
  
## <a name="external-components-that-follow-a-lifecycle-policy-other-than-the-visual-studio-policy"></a>遵循生命周期策略而不是 Visual Studio 策略的外部组件  
 下表列出了 Visual Studio 可能随附的 Microsoft 平台组件（具体取决于 Visual Studio 软件的特定版本），它们遵循自己的支持策略和时间范围。  
  
|产品系列|外部名称|  
|--------------------|-------------------|  
|[.NET 3.5](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=net%20framework%203.5&Filter=FilterNO)|.NET 3.5 SDK<br /><br /> Windows Identity Foundation|  
|[.NET 4.5](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=net%20framework%204.5&Filter=FilterNO)|.NET 4.5 SDK|  
|[.NET 4.5.1](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=.NET%20Framework%204.5.1&Filter=FilterNO)|.NET 4.5.1 MT Pack（经典）<br /><br /> .NET 4.5.1 Multi-targeting Pack（应用商店）<br /><br /> .NET 4.5.1 OOB MSU<br /><br /> .NET 4.5.1 Redist<br /><br /> .NET 4.5.1 Redist 语言包<br /><br /> .NET 4.5.1 SDK|  
|[ASP.NET Web 堆栈](http://go.microsoft.com/fwlink/?LinkId=328918)|ASP.NET MVC 4<br /><br /> ASP.NET MVC 5<br /><br /> ASP.NET Web API<br /><br /> ASP.NET Web API 2<br /><br /> ASP.NET 网页 2<br /><br /> ASP.NET 网页 3|  
|[Entity Framework 6](http://go.microsoft.com/fwlink/?LinkId=328950)|Entity Framework 6|  
|[Exchange 2013](http://go.microsoft.com/fwlink/?LinkId=328950)|Exchange Web 服务|  
|[Microsoft OWIN](http://go.microsoft.com/fwlink/?LinkId=328951)|Microsoft OWIN|  
|[Microsoft Web 开发人员工具 2013](http://go.microsoft.com/fwlink/?LinkId=328952)|Microsoft Web 开发人员工具 2013|  
|这些组件的更新通过 NuGet 分发，并且不遵循标准 Microsoft 生命周期策略。  有关详细信息，请参阅 [http://docs.nuget.org/](http://docs.nuget.org/)。|适用于 Microsoft.NET Framework 4.5 的 JSON Web 令牌处理程序<br /><br /> NuGet 2.7<br /><br /> SignalR<br /><br /> Web 优化框架<br /><br /> WebGrease|  
|[ODataLib](http://go.microsoft.com/fwlink/?LinkId=328954)|ODataLib|  
|[Office 2013](http://support.microsoft.com/lifecycle/?p1=16674)|Open XML SDK|  
|[Online Services 策略](http://support.microsoft.com/gp/OSSLpolicy)|Microsoft Ads SDK|  
|[SharePoint 2013](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=sharepoint%20server%202013&Filter=FilterNO)|SharePoint 客户端组件<br /><br /> SharePoint Foundation 2013<br /><br /> Windows Identity Foundation 扩展|  
|[Silverlight 5](http://support.microsoft.com/lifecycle/?p1=16278)<br /><br /> <br />> 另请参阅：[http://support.microsoft.com/gp/lifean45](http://support.microsoft.com/gp/lifean45)|Silverlight 5 运行时<br /><br /> Silverlight 5 SDK|  
|[SQL Server 2008 R2](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=SQL%20Server%202008%20R2&Filter=FilterNO)|SQL 系统 CLR 类型 (SQL Server 2008 R2)|  
|[SQL Server 2012](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=SQL%20Server%202012&Filter=FilterNO)|DACFx (DACFramework)<br /><br /> SMO (SharedManagementObjects)<br /><br /> SQL 命令行实用工具<br /><br /> SQL 语言服务 - IntelliSense (TSQLLanguageService)<br /><br /> SQL LocalDB<br /><br /> SQL Native Client (Sqlncli)<br /><br /> SQL Server Express 2012 SP1<br /><br /> SQL System CLR Types (SQL Server 2012)<br /><br /> SQLDOM|  
|[SQL Server 2014](https://support.microsoft.com/lifecycle/search?sort=PN&alpha=SQL%20Server%202014&Filter=FilterNO)|DACFx (DACFramework)<br /><br /> SMO (SharedManagementObjects)<br /><br /> SQL 命令行实用工具<br /><br /> SQL 语言服务 - IntelliSense (TSQLLanguageService)<br /><br /> SQL LocalDB<br /><br /> SQL Native Client (Sqlncli)<br /><br /> SQL Server Express 2014<br /><br /> SQL 系统 CLR 类型 (SQL Server 2014)<br /><br /> SQLDOM|  
|[SQL Server Compact Edition 4.0](http://support.microsoft.com/lifecycle/?p1=16106)|SQL Server Compact Edition 4.0|  
|[WCF RIA Services v1.0 SP2](http://go.microsoft.com/fwlink/?LinkId=328955)|WCF RIA Services v1.0 SP2|  
|[Windows Server 2008](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows%20Server%202008&Filter=FilterNO)|适用于 Windows Server 2008 的 Windows Web 服务 (WWS)|  
|[Windows 7](http://support.microsoft.com/lifecycle/?c2=14019)|Windows 7 SDK|  
|[Windows 8](http://support.microsoft.com/lifecycle/?c2=16796)|Windows 8 SDK|  
|[Windows 8.1](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=windows%208.1&Filter=FilterNO)|Windows 8.1 SDK<br /><br /> Windows JavaScript 库 (WinJS)|  
|[Microsoft Azure](http://support.microsoft.com/gp/azure-cloud-lifecycle-faq)<br /><br /> <br />> 另请参阅：[在线生命周期策略](http://support.microsoft.com/gp/OSSLpolicy)|Microsoft Azu re 移动服务 SDK<br /><br /> Microsoft Azure 移动服务工具|