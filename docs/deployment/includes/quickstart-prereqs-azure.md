---
ms.openlocfilehash: 6c210537c671ef6960d3f767c740dee5c1538fac
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "70197101"
---
## <a name="prerequisites"></a>先决条件

::: moniker range=">=vs-2019"

* 安装有 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) 并具有所选语言相应的工作负载：
  * ASP.NET：**ASP.NET 和 Web 开发**
  * Node.js：  Node.js 开发
::: moniker-end
::: moniker range="vs-2017"
* 安装有 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)并具有所选语言相应的工作负荷：
  * ASP.NET：**ASP.NET 和 Web 开发**
  * Node.js：  Node.js 开发
::: moniker-end

* Azure 订阅。 如果还没有订阅，请[免费注册](https://azure.microsoft.com/free/dotnet/)，其中包括为期 30 天的 $200 额度和为期 12 个月的热门免费服务。

* ASP.NET、ASP.NET Core、.NET Core 或 Node.js 项目。 如果还没有项目，请选择下方选项：
  * ASP.NET Core：请遵照[快速入门：使用 Visual Studio 创建首个 ASP.NET Core Web 应用](../../ide/quickstart-aspnet-core.md)进行操作，或使用“文件” > “新建项目”，选择“Visual C#” > “.NET Core”，然后选择“ASP.NET Core Web 应用程序”      。 系统出现提示时，请选择“Web 应用程序(模型-视图-控制器)”模板，确保选中“无身份验证”，然后选择“确定”    。
  * Node.js：请遵照[快速入门：使用 Visual Studio 创建首个 Node.js 应用](../../ide/quickstart-nodejs.md)进行操作，或使用“文件” > “新建文件”，选择“JavaScript”，然后选择“空白 Node.js Web 应用程序”     。

* 请确保在执行部署步骤之前，使用“生成”>“生成解决方案”菜单命令生成项目  。