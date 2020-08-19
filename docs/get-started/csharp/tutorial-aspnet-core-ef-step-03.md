---
title: 步骤 3：在 ASP.NET Core 应用中处理数据
description: 通过此视频教程和分步说明开始在 ASP.NET Core Web 应用中使用 Entity Framework Core 来处理数据。
ms.custom: get-started
ms.date: 03/31/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
monikerRange: vs-2019
ms.topic: tutorial
ms.devlang: CSharp
author: ardalis
ms.author: ornella
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: 42bc0442dc5901f92fc8a83b7af41c1fc42f4be4
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88250797"
---
# <a name="step-3-work-with-data-using-entity-framework"></a>步骤 3：使用实体框架处理数据

请按照下列步骤开始在 ASP.NET Core Web 应用中使用 Entity Framework Core 来处理数据。

观看此视频，按照说明将数据添加到你的首个 ASP.NET Core 应用。 

> [!VIDEO https://www.youtube.com/embed/dulJCwNrqhM]

## <a name="open-your-project"></a>打开项目

如果正在学习这些视频，请打开在上一节中创建的 Web 应用程序项目。 如果从这里开始，需要创建一个新项目并选择“ASP.NET Web 应用程序”  ，然后选择“Web 应用程序”  。 将其余选项保留为默认设置。

## <a name="add-your-model"></a>添加模型

若要处理 ASP.NET Core 应用程序中的数据，首先要描述数据应该是什么样的。 我们将上述过程称之为为要解决的问题中所涉及的内容创建一个模型  。 在实际应用程序中，我们将向这些模型添加自定义业务逻辑，以便它们能够以特定方式运行，并为我们自动执行任务。 对于此示例，我们将创建一个用于跟踪棋盘游戏的简单系统。 我们需要一个代表游戏的类，它包含一些我们可能想要记录的关于该游戏的属性，比如它可以支持多少个玩家。 此类将进入一个我们将在 Web 项目的根目录中创建的新文件夹，称为“Models”  。

```csharp
public class Game
{
    public int Id { get; set; }
    public string Title { get; set; }
    public int PublicationYear { get; set; }
    public int MinimumPlayers { get; set; }
    public int MaximumPlayers { get; set; }
}
```

## <a name="create-the-pages-to-manage-your-game-library"></a>创建页面来管理游戏库

现在我们已经准备好创建将用于管理游戏库的页面。 这听起来可能有点吓人，但实际上非常简单。 首先，我们需要决定应将此功能放在应用中的哪个位置。 打开 Web 项目中的“Pages”文件夹，并在其中添加一个新文件夹。 称之为“Games”  。

现在右键单击“Games”并选择“添加”   > “新搭建基架的项目”  。 使用“实体框架(CRUD)”  选项选择 Razor Pages。 CRUD 代表“创建、读取、更新、删除”，此模板将为上述每个操作创建页面（包括“列出所有”页和“查看一个项目的详细信息”页）。

![Visual Studio 2019 ASP.NET Core 添加已搭建基架页](media/vs-2019/vs2019-add-scaffold.png)

选择游戏模型类并使用“+”图标添加一个新的数据上下文类。 将其命名为 `AppDbContext`。 其余部分保留为默认设置，然后单击“添加”  。

你将看到以下 Razor Pages 添加到 Games 文件夹中：

- Create.cshtml
- Delete.cshtml
- Details.cshtml
- Edit.cshtml
- Index.cshtml

![Visual Studio 2019 ASP.NET Core 已搭建基架页](media/vs-2019/vs2019-scaffolded-pages.png)

除了在“Games”  文件夹中添加页面，基架操作还向我的 startup.cs  类添加了代码。 查看此类中的 `ConfigureServices` 方法，你会看到添加了以下代码：

```csharp
services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(Configuration.GetConnectionString("AppDbContext")));
```

还会发现 `AppDbContext` 连接字符串已添加到项目的“appsettings.json”  文件。

如果现在运行应用，它可能会失败，因为尚未创建数据库。 如果需要，可以将应用配置为自动创建数据库，方法是[将一些代码添加到 Program.cs](/aspnet/core/data/ef-rp/intro?view=aspnetcore-2.1&tabs=visual-studio#update-main)：

```csharp
public static void Main(string[] args)
{
    var host = CreateWebHostBuilder(args).Build();

    using (var scope = host.Services.CreateScope())
    {
        var services = scope.ServiceProvider;

        try
        {
            var context = services.GetRequiredService<Data.AppDbContext>();
            context.Database.EnsureCreated();
        }
        catch (Exception ex)
        {
            var logger = services.GetRequiredService<ILogger<Program>>();
            logger.LogError(ex, "An error occurred creating the DB.");
        }
    }

    host.Run();
}
```

要解析上述代码中的类型名，请在现有的 using 语句块的末尾将以下 using 语句添加到 Program.cs  ：

```csharp
using Microsoft.Extensions.DependencyInjection;
using WebApplication1.Models;
```

请务必在代码中使用项目名称而不是 WebApplication1。

大部分代码仅用于错误处理，并在应用运行之前提供对 EF Core `AppDbContext` 的访问。 重要的行是显示 `context.Database.EnsureCreated()` 的行，如果尚不存在数据库，则将创建一个。 现在已准备好运行应用。

## <a name="test-it-out"></a>测试应用

运行应用程序并导航到地址栏中的 `/Games`。 你将看到一个空列表页。 单击“新建”  以向集合添加一个新的 `Game`。 填写表单并单击“创建”  。 应在列表视图中看到它。 单击“详细信息”  以查看单个记录的详细信息。

添加另一个记录。 可以单击“编辑”  以更改记录的详细信息，或单击“删除”  删除记录，系统将在实际删除该记录之前提示你进行确认。

![浏览器中的 Visual Studio 2019 ASP.NET Core 已搭建基架页](media/vs-2019/vs2019-game-list.png)

这就是使用 EF Core 和 Visual Studio 2019 来着手处理 ASP.NET Core 应用中的数据所需的一切操作。

## <a name="next-steps"></a>后续步骤

在下一个视频中，你将了解如何将 Web API 支持添加到应用。

[步骤 4：从 ASP.NET Core 应用中公开 Web API](tutorial-aspnet-core-ef-step-04.md)

## <a name="see-also"></a>请参阅

- [在 ASP.NET Core 中结合使用 Razor Pages 和 Entity Framework Core](/aspnet/core/data/ef-rp/intro?view=aspnetcore-2.1&tabs=visual-studio)
- [ASP.NET Core Razor Pages 和 EF Core](/aspnet/core/data/?view=aspnetcore-2.1)
