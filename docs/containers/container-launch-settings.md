---
title: Visual Studio 容器工具启动设置
author: ghogen
description: 容器工具生成过程概述
ms.author: ghogen
ms.date: 08/15/2019
ms.technology: vs-azure
ms.topic: conceptual
ms.openlocfilehash: b8c732fb847e4d9944e0d6a5405a29e7879cbdc9
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75400866"
---
# <a name="container-tools-launch-settings"></a>容器工具启动设置

在 ASP.NET Core 项目的“属性”文件夹中，可以找到 launchSettings.json 文件，其中包含用于控制如何在开发计算机上启动 Web 应用的设置  。 有关如何在 ASP.NET 开发中使用此文件的详细信息，请参阅[在 ASP.NET Core 中使用多个环境](/aspnet/core/fundamentals/environments?view=aspnetcore-2.2)。 在“launchSettings.json”中，Docker 部分中的设置与 Visual Studio 处理容器化应用的方式相关   。

::: moniker range="vs-2017"
```json
    "Docker": {
      "commandName": "Docker",
      "launchBrowser": true,
      "launchUrl": "{Scheme}://{ServiceHost}:{ServicePort}"
    }
```

::: moniker-end
::: moniker range=">=vs-2019"

```json
    "Docker": {
      "commandName": "Docker",
      "launchBrowser": true,
      "launchUrl": "{Scheme}://{ServiceHost}:{ServicePort}",
      "environmentVariables": {
        "ASPNETCORE_URLS": "https://+:443;http://+:80",
        "ASPNETCORE_HTTPS_PORT": "44360"
      },
      "httpPort": 51803,
      "useSSL": true,
      "sslPort": 44360
    }
```

::: moniker-end

commandName 设置确定此部分是否适用于容器工具。 下表显示了可在此部分中设置的属性：

::: moniker range="vs-2017"

|设置名|Version|示例|描述|
|------------|-------|-------|---------------|
|launchBrowser|Visual Studio 2017|"launchBrowser": true|指示在成功启动项目后是否启动浏览器。|
|launchUrl|Visual Studio 2017|"launchUrl": "\<scheme>://\<serviceHost>:\<servicePort>"|启动浏览器时使用该 URL。  此字符串支持的替换令牌为：<br>   \<方案> - 根据是否使用 SSL 将其替换为“http”或“https”。<br>   \<serviceHost > - 通常替换为“localhost”。 但是，面向使用 Windows 10 RS3 或更低版本的 Windows 容器时，将其替换为容器的 IP。<br>   \<servicePort> - 通常根据是否使用 SSL 将其替换为 sslPort 或 httpPort。  但是，在面向使用 Windows 10 RS3 或更低版本的 Windows 容器时，根据是否使用 SSL 将其替换为“443”或“80”。|

::: moniker-end

::: moniker range=">=vs-2019"

| 设置名         | 示例                                               | 描述                                                                                                             |
| -------------------- | ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| commandLineArgs      | "commandLineArgs": "--mysetting myvalue"              | 在容器中启动项目时使用这些命令行参数。                                     |
| environmentVariables | "environmentVariables": {                             | 在容器中启动时，这些环境变量值将传递给该过程。                       |
|                      | "ASPNETCORE_URLS": "https://+:443; http://+:80",       |                                                                                                                         |
|                      | "ASPNETCORE_HTTPS_PORT":"44381"                      |                                                                                                                         |
|                      | }                                                     |                                                                                                                         |
| httpPort             | "httpPort":24051                                     | 启动容器时，主机上的此端口映射到容器的端口 80。                                |
|                      |                                                       | 如果未指定，则该值取自 iisSettings 值。                                                          |
| launchBrowser        | "launchBrowser": true                                 | 指示在成功启动项目后是否启动浏览器。                                       |
| launchUrl            | "launchUrl": "<scheme>://<serviceHost>:<servicePort>" | 启动浏览器时使用该 URL。 此字符串支持的替换令牌为：                          |
|                      |                                                       | - <scheme> - 根据是否使用 SSL 将其替换为“http”或“https”。                                   |
|                      |                                                       | - <serviceHost> - 通常替换为“localhost”。                                                                    |
|                      |                                                       | 但是，面向使用 Windows 10 RS3 或更低版本的 Windows 容器时，将其替换为容器的 IP。           |
|                      |                                                       | - <servicePort> - 通常根据是否使用 SSL 将其替换为 sslPort 或 httpPort。                   |
|                      |                                                       | 但是，面向使用 Windows 10 RS3 或更低版本的 Windows 容器时，将其替换为“443”或“80”，         |
|                      |                                                       | 具体取决于是否使用 SSL。                                                                                       |
| sslPort              | "sslPort":44381                                      | 启动容器时，主机上的此端口映射到容器的端口 443。                               |
|                      |                                                       | 如果未指定，则该值取自 iisSettings 值。                                                          |
| useSSL               | "useSSL": true                                        | 指示在启动项目时是否使用 SSL。 如果未指定 useSSL，则在 sslPort 大于 0 时使用 SSL。 |

::: moniker-end

## <a name="next-steps"></a>后续步骤

通过设置[容器工具生成属性](container-msbuild-properties.md)来配置项目。

## <a name="see-also"></a>请参阅

[Docker Compose 生成属性](docker-compose-properties.md)
