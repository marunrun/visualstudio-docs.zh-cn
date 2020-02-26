---
title: 步骤 4：从 ASP.NET Core 应用中公开 Web API
description: 通过此视频教程和分步说明将 Web API 添加到 ASP.NET Core Web 应用。
ms.custom: get-started
ms.date: 02/13/2020
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
ms.openlocfilehash: 5ea9468bdf86986ab542fb1cabc873c9aeb75fd6
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77580035"
---
# <a name="step-4-expose-a-web-api-from-your-aspnet-core-app"></a>步骤 4：从 ASP.NET Core 应用中公开 Web API

请按照下列步骤将 Web API 添加到现有的 ASP.NET Core 应用。

观看此视频，按照说明向你的首个 ASP.NET Core 应用添加 Web API 支持。 

> [!VIDEO https://www.youtube.com/embed/o_fYPOsAXts]

## <a name="open-your-project"></a>打开项目

在 Visual Studio 2019 中打开 ASP.NET Core 应用。 应用应该已在使用 EF Core 来管理模型类型，如[本系列教程步骤 3](tutorial-aspnet-core-ef-step-03.md) 中所配置的那样。

## <a name="add-an-api-controller"></a>添加 API 控制器

右键单击项目并添加一个名为“Api”  的新文件夹。 然后，右键单击文件夹并选择“添加”   > “新搭建基架的项目”  。 选择“其操作使用实体框架的 API 控制器”。  现在选择现有模型类，然后单击“添加”  。

![Visual Studio 2019 ASP.NET Core 已搭建 API 控制器基架](media/vs-2019/vs2019-add-scaffold-api.png)

## <a name="reviewing-the-generated-controller"></a>查看生成的控制器

生成的代码包括一个新的控制器类。 在类定义的顶部有两个属性。

```csharp
[Route("api/[controller]")]
[ApiController]
public class GamesController : ControllerBase
```

第一个属性指定控制器中的操作路由为 `api/[controller]`，意味着如果控制器名为 `GamesController`，则路由为 `api/Games`。

第二个属性 `[ApiController]` 向类添加了一些有用的验证，比如确保每个操作方法都包含其自己的 `[Route]` 属性。

```csharp
public class GamesController : ControllerBase
{
    private readonly AppDbContext _context;

    public GamesController(AppDbContext context)
    {
        _context = context;
    }
```

控制器使用现有的 `AppDbContext`，它被传递到其构造函数中。 每个操作将使用此字段来处理应用程序的数据。

```csharp
// GET: api/Games
[HttpGet]
public IEnumerable<Game> GetGame()
{
    return _context.Game;
}
```

第一种方法是简单的 GET 请求，使用 `[HttpGet]` 属性指定。 它不带任何参数，并返回数据库中所有游戏的列表。

```csharp
// GET: api/Games/5
[HttpGet("{id}")]
public async Task<IActionResult> GetGame([FromRoute] int id)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }

    var game = await _context.Game.FindAsync(id);

    if (game == null)
    {
        return NotFound();
    }

    return Ok(game);
}
```

下一个方法指定路由中的 `{id}`，它将被添加到 `/` 之后的路由中，因此完整的路由将类似于 `api/Games/5`，如顶部注释所示。 `id` 输入映射到该方法的 `id` 参数。 在此方法中，如果模型无效，则返回 `BadRequest` 结果。 否则，EF 将尝试查找与所提供的 `id` 匹配的记录。 如果找不到，则返回 `NotFound` 结果，反之返回相应的 `Game` 记录。

```csharp
// PUT: api/Games/5
[HttpPut("{id}")]
public async Task<IActionResult> PutGame([FromRoute] int id, [FromBody] Game game)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }

    if (id != game.Id)
    {
        return BadRequest();
    }

    _context.Entry(game).State = EntityState.Modified;

    try
    {
        await _context.SaveChangesAsync();
    }
    catch (DbUpdateConcurrencyException)
    {
        if (!GameExists(id))
        {
            return NotFound();
        }
        else
        {
            throw;
        }
    }

    return NoContent();
}
```

下一步，向 API 发出的 `[HttpPut]` 请求用于执行更新。 新的 `Game` 记录在请求正文中提供。 将执行一些验证和错误检查，如果一切顺利，将使用请求正文中提供的值对数据库中的记录进行更新。 否则返回相应的错误响应。

```csharp
// POST: api/Games
[HttpPost]
public async Task<IActionResult> PostGame([FromBody] Game game)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }

    _context.Game.Add(game);
    await _context.SaveChangesAsync();

    return CreatedAtAction("GetGame", new { id = game.Id }, game);
}
```

`[HttpPost]` 请求用于向系统添加新记录。 与使用 `[HttpPut]` 一样，记录会被添加到请求正文中。 如果有效，EF Core 会将记录添加到数据库中，且操作返回更新后的记录（带有其数据库生成的ID）和指向 API 中记录的链接。

```csharp
// DELETE: api/Games/5
[HttpDelete("{id}")]
public async Task<IActionResult> DeleteGame([FromRoute] int id)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }

    var game = await _context.Game.FindAsync(id);
    if (game == null)
    {
        return NotFound();
    }

    _context.Game.Remove(game);
    await _context.SaveChangesAsync();

    return Ok(game);
}
```

最后，将 `[HttpDelete]` 路由与 ID 结合使用以删除一条记录。 如果请求有效以及存在具有给定 ID 的记录，EF Core 将从数据库中删除它。

## <a name="adding-swagger"></a>添加 Swagger

Swagger 是一个 API 文档兼测试工具，可以作为一组服务和中间件添加到 ASP.NET Core 应用。 为此，右键单击项目，然后选择“管理 NuGet 包”  。 然后，单击“浏览”，搜索 `Swashbuckle.AspNetCore`，并安装 4.0.1 版本  。

![Visual Studio 2019 从 Nuget 添加 Swashbuckle](media/vs-2019/vs2019-nuget-swashbuckle.png)

安装后，打开 `Startup.cs` 并将以下内容添加到 `ConfigureServices` 方法末尾：

```csharp
services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new Info { Title = "My API", Version = "v1" });
});
```

还需要在文件顶部添加 `using Swashbuckle.AspNetCore.Swagger;`。

接下来，在 `UseMvc` 前向 `Configure` 方法添加以下内容：

```csharp
// Enable middleware to serve generated Swagger as a JSON endpoint.
app.UseSwagger();

// Enable middleware to serve swagger-ui (HTML, JS, CSS, etc.), 
// specifying the Swagger JSON endpoint.
app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
});
```

现在，应能够生成并运行应用。 在浏览器中，导航到地址栏中的 `/swagger`。 应看到应用 API 终结点和模型的列表。 

![浏览器中的 Visual Studio 2019 Swagger 页](media/vs-2019/vs2019-swagger-browser.png)

单击“游戏”下的终结点，然后单击 `Try it out` 和 `Execute`，查看不同终结点的行为方式。

## <a name="next-steps"></a>后续步骤

下一个视频中将介绍如何将应用部署到 Azure。

[步骤 5：将 ASP.NET Core 应用部署到 Azure](tutorial-aspnet-core-ef-step-05.md)

## <a name="see-also"></a>请参阅

- [Swashbuckle 和 ASP.NET Core 入门](/aspnet/core/tutorials/getting-started-with-swashbuckle?view=aspnetcore-2.2&tabs=visual-studio)
- [带有 Swagger/OpenAPI 的 ASP.NET Core Web API 帮助页](/aspnet/core/tutorials/web-api-help-pages-using-swagger?view=aspnetcore-2.2)