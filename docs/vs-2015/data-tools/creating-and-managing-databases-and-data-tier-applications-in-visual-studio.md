---
title: 创建和管理数据库和数据层应用程序
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
helpviewer_keywords:
- managing change, databases
- database features of Visual Studio, managing change
- databases, managing change
- managing change, database servers
ms.assetid: 40b51f5a-d52c-44ac-8f84-037a0917af33
caps.latest.revision: 40
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d6cb4a3beb12d2b33b8b13441df66116fe449d09
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431157"
---
# <a name="creating-and-managing-databases-and-data-tier-applications-in-visual-studio"></a>创建和管理数据库和 Visual Studio 中的数据层应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

重要提示
> 早期版本中包含的数据库项目[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中现在提供[!INCLUDE[sql_Denali_long](../includes/sql-denali-long-md.md)]工具。 有关详细信息，请参阅[SQL Server 开发人员工具](http://go.microsoft.com/fwlink/?LinkId=228126)。

 可以使用数据库项目来创建新数据库，新的数据层应用程序 (Dac)，以及更新现有数据库和数据层应用程序。 数据库项目和 DAC 项目，可以大致相同的方式将这些技术应用于托管或本机代码中将版本控制和项目管理技术应用于进行数据库开发工作。 可帮助开发团队通过创建管理数据库和数据库服务器将变为*DAC 项目*，*数据库项目*，或*服务器项目*并将其置于在版本控制。 你的团队成员可以然后签出文件，以使、 生成和测试中的更改*隔离的开发环境*，或沙盒之前与团队共享它们。 若要帮助确保代码质量，你的团队可以完成并部署到生产环境的更改之前在过渡环境中测试的特定版本的数据库的所有更改。

 有关支持的数据层应用程序的数据库功能的列表，请参阅[数据层应用程序中支持的功能](http://go.microsoft.com/fwlink/?LinkId=164239)在 Microsoft 网站上。 如果您使用您的数据库不支持的数据层应用程序的功能，您应改用数据库项目来管理对你的数据库的更改。

## <a name="common-high-level-tasks"></a>常见的高级任务

|高级任务|支持内容|
|----------------------|------------------------|
|**启动数据层应用程序的开发：** DAC 是随引入的新概念[!INCLUDE[sskatmai_r2](../includes/sskatmai-r2-md.md)]，其中包含用于定义[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]数据库和支持实例使用的客户端-服务器或第 3 层应用程序对象。 DAC 包括数据库对象，如表和视图，以及实例实体，例如登录名。 可以使用[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]若要创建一个 DAC 项目，生成一个 DAC 包文件，并将该 DAC 包文件发送到部署到的实例上的数据库管理员[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]数据库引擎。|-   [创建和管理数据层应用程序](http://go.microsoft.com/fwlink/?LinkId=160741)（Microsoft 网站）<br />-   [SQL Server Management Studio](http://go.microsoft.com/fwlink/?LinkId=227328)|
|**执行迭代数据库开发：** 如果你是开发人员或测试人员，您签出项目的部分，然后独立的开发环境中对它们进行更新。 通过使用此类型的环境，可以测试所做的更改，而不影响其他团队的成员。 所做的更改完成后，您将签入版本控制，其他团队成员可以获取所做的更改和生成并将其部署到测试服务器文件。|-   [查询和文本编辑器 (SQL Server Management Studio)](http://go.microsoft.com/fwlink/?LinkId=227327) （Microsoft 网站）<br />-   [TRANSACT-SQL 调试器](http://go.microsoft.com/fwlink/?LinkId=227324)（Microsoft 网站）|
|**原型制作，验证测试结果和修改数据库脚本和对象：** 可以使用[!INCLUDE[tsql](../includes/tsql-md.md)]编辑器来执行这些常见任务之一。|-   [查询和文本编辑器 (SQL Server Management Studio)](http://go.microsoft.com/fwlink/?LinkId=227327) （Microsoft 网站）|

## <a name="see-also"></a>请参阅
 [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
