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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2d6ed13f2e21ea6b9da82eb47afefdd16088e71d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672471"
---
# <a name="creating-and-managing-databases-and-data-tier-applications-in-visual-studio"></a>在 Visual Studio 中创建和管理数据库和数据层应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

重要提示
> @No__t_1 工具中现在提供了 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 早期版本中包含的数据库项目。 有关详细信息，请参阅[SQL Server Developer 工具](http://go.microsoft.com/fwlink/?LinkId=228126)。

 您可以使用数据库项目创建新的数据库、新的数据层应用程序（Dac）以及更新现有的数据库和数据层应用程序。 使用数据库项目和 DAC 项目，您可以将版本控制和项目管理技术应用于您的数据库开发工作，就像将这些技术应用于托管代码或本机代码一样。 您可以通过创建*DAC 项目*、*数据库项目*或*服务器项目*并将其置于版本控制下，帮助您的开发团队管理对数据库和数据库服务器所做的更改。 然后，你的团队成员可以在将其与团队共享之前，先签出文件，以便在*隔离开发环境*或沙盒中生成和测试更改。 为了帮助确保代码质量，你的团队可以在将更改部署到生产环境之前，在过渡环境中完成并测试该数据库的特定版本的所有更改。

 有关数据层应用程序支持的数据库功能的列表，请参阅 Microsoft 网站上的[数据层应用程序中支持的功能](http://go.microsoft.com/fwlink/?LinkId=164239)。 如果你在数据库中使用数据层应用程序不支持的功能，则应改为使用数据库项目来管理对数据库的更改。

## <a name="common-high-level-tasks"></a>常见的高级任务

|高级任务|支持内容|
|----------------------|------------------------|
|**开始开发数据层应用程序：** DAC 是 [!INCLUDE[sskatmai_r2](../includes/sskatmai-r2-md.md)] 引入的一种新概念，其中包含 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库的定义和客户端-服务器或3层应用程序使用的支持实例对象。 DAC 包括数据库对象（如表和视图）以及实例实体（例如登录名）。 您可以使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 来创建一个 DAC 项目，生成一个 DAC 包文件，然后将该 DAC 包文件发送到数据库管理员，以便部署到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库引擎的实例上。|-   [创建和管理数据层应用程序](http://go.microsoft.com/fwlink/?LinkId=160741)（Microsoft 网站）<br />-   [SQL Server Management Studio](http://go.microsoft.com/fwlink/?LinkId=227328)|
|**执行迭代数据库开发：** 如果你是开发人员或测试人员，请签出项目的各个部分，然后在隔离的开发环境中对其进行更新。 通过使用这种类型的环境，您可以测试您的更改，而不会影响团队的其他成员。 更改完成后，可将文件签回版本控制中，其他团队成员可在其中获取所做的更改并将其生成并部署到测试服务器。|-   [查询和文本编辑器（SQL Server Management Studio）](http://go.microsoft.com/fwlink/?LinkId=227327) （Microsoft 网站）<br />-   [Transact-sql 调试器](http://go.microsoft.com/fwlink/?LinkId=227324)（Microsoft 网站）|
|**原型制作，验证测试结果，修改数据库脚本和对象：** 您可以使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 编辑器执行其中的一项常见任务。|-   [查询和文本编辑器（SQL Server Management Studio）](http://go.microsoft.com/fwlink/?LinkId=227327) （Microsoft 网站）|

## <a name="see-also"></a>请参阅
 [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
