---
title: 在 Azure 应用服务 (Windows) 上配置 Python
description: 如何在 Azure 应用服务上安装 Python 解释器和库，并配置 Web 应用程序，以正确引用该解释器。
ms.date: 01/07/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: 7ffe0de939eba8af38c132fc3de5c96a9499e3f0
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62535926"
---
# <a name="how-to-set-up-a-python-environment-on-azure-app-service-windows"></a>如何在 Azure 应用服务 (Windows) 上设置 Python 环境

> [!Important]
> 如本文所述，Microsoft 已弃用 Windows 上的应用服务适用的 Python 扩展，改为支持直接部署到 [Linux 上的应用服务](publishing-python-web-applications-to-azure-from-visual-studio.md)。

[Azure App Service](https://azure.microsoft.com/services/app-service/) 是适用于 Web 应用的平台即服务产品/服务，这些应用包括通过浏览器访问的站点、用户自己的客户端使用的 REST API 或事件触发的处理过程。 应用服务完全支持使用 Python 实现应用。

Azure 应用服务的可自定义 Python 支持作为一组应用服务站点扩展来提供，其中每个扩展均包含特定版本的 Python 运行时  。 如本文所述，随后可以将任何所需的包直接安装到该环境中。 通过自定义应用服务自身中的环境，你无需维护 Web 应用项目中的包，也无需使用应用代码上传这些包。

> [!Tip]
> 默认情况下，虽然应用服务在服务器上的根文件夹中安装了 Python 2.7 和 Python 3.4，但是不能在这些环境中自定义或安装包，也不应依赖于它们的存在。 如本文所述，应依赖于控制的站点扩展。

## <a name="choose-a-python-version-through-the-azure-portal"></a>通过 Azure 门户选择 Python 版本

1. 在 Azure 门户中创建 Web 应用的应用服务
1. 在“应用服务”页上，向下滚动到“开发工具”部分，选择“扩展”，然后选择“+ 添加”    。
1. 在列表中，向下滚动到包含所需 Python 版本的扩展：

    ![显示 Python 扩展的 Azure 门户](media/python-on-azure-extensions.png)

    > [!Tip]
    > 如果需要较早版本的 Python，并且未看到它列在站点扩展中，仍可以通过 Azure 资源管理器进行安装，如下一节所述。

1. 选择该扩展，接受法律条款，然后选择“确定”  。
1. 安装完成后，门户中会显示通知。

## <a name="choose-a-python-version-through-the-azure-resource-manager"></a>通过 Azure 资源管理器选择 Python 版本

如果要使用 Azure 资源管理器模板部署应用服务，请将站点扩展添加为资源。 具体而言，此扩展显示为一个嵌套资源（`resources` 下的 `resources` 对象），其类型为 `siteextensions`，名称来源于 [siteextensions.net](https://www.siteextensions.net/packages?q=Tags%3A%22python%22)。

例如，添加对 `python361x64` (Python 3.6.1 x64) 的引用后，模板外观可能如下所示（省略了某些属性）：

```json
"resources": [
  {
    "apiVersion": "2015-08-01",
    "name": "[parameters('siteName')]",
    "type": "Microsoft.Web/sites",

    // ...

    "resources": [
      {
        "apiVersion": "2015-08-01",
        "name": "python361x64",
        "type": "siteextensions",
        "properties": { },
        "dependsOn": [
          "[resourceId('Microsoft.Web/sites', parameters('siteName'))]"
        ]
      },
      // ...
    ]
  }
```

## <a name="set-webconfig-to-point-to-the-python-interpreter"></a>将 web.config 设置为指向 Python 解释器

（通过门户或 Azure 资源管理器模板）安装站点扩展后，接下来将应用的 web.config  文件指向 Python 解释器。 web.config 文件指示在应用服务上运行的 IIS (7+) Web 服务器如何通过 HttpPlatform（推荐）或 FastCGI 处理 Python 请求  。

首先找到站点扩展程序 python.exe  的完整路径，然后创建并修改相应的 web.config  文件。

### <a name="find-the-path-to-pythonexe"></a>找到 python.exe 的路径

Python 站点扩展安装在 d:\home  下服务器上的文件夹中，适合 Python 版本和体系结构（几个较早版本的情况除外）。 例如，Python 3.6.1 x64 安装在 d:\home\python361x64  中。 到 Python 解释器的完整路径则为 d:\home\python361x64\python.exe  。

若要查看应用服务上的特定路径，请在“应用服务”页上选择“扩展”，然后选择列表中的扩展  。

![Azure App Service 上的扩展列表](media/python-on-azure-extension-list.png)

此操作打开包含此路径的扩展描述页：

![Azure App Service 上的扩展详细信息](media/python-on-azure-extension-detail.png)

如果查看扩展路径时遇到问题，可以使用控制台手动找到它：

1. 在“应用服务”页上，选择“开发工具”   > “控制台”  。
1. 输入命令 `ls ../home` 或 `dir ..\home` 查看顶级扩展文件夹，例如 Python361x64  。
1. 输入一个类似于 `ls ../home/python361x64` 或 `dir ..\home\python361x64` 的命令，确认该文件夹包含 python.exe  和其他解释器文件。

### <a name="configure-the-httpplatform-handler"></a>配置 HttpPlatform 处理程序

HttpPlatform 模块将套接字连接直接传递到独立的 Python 进程。 借助此传递可根据需要运行任何 Web 服务器，但需要用于运行本地 Web 服务器的启动脚本。 在 web.config 的 `<httpPlatform>` 元素中指定脚本，其中 `processPath` 属性指向站点扩展的 Python 解释器，`arguments` 属性指向脚本和希望提供的任何参数：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="PythonHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified"/>
    </handlers>
    <httpPlatform processPath="D:\home\Python361x64\python.exe"
                  arguments="D:\home\site\wwwroot\runserver.py --port %HTTP_PLATFORM_PORT%"
                  stdoutLogEnabled="true"
                  stdoutLogFile="D:\home\LogFiles\python.log"
                  startupTimeLimit="60"
                  processesPerApplication="16">
      <environmentVariables>
        <environmentVariable name="SERVER_PORT" value="%HTTP_PLATFORM_PORT%" />
      </environmentVariables>
    </httpPlatform>
  </system.webServer>
</configuration>
```

此处显示的 `HTTP_PLATFORM_PORT` 环境变量包含端口，本地服务器使用该端口侦听来自 localhost 的连接。 此示例还演示如何根据需要创建其他环境变量，本示例中为 `SERVER_PORT`。

### <a name="configure-the-fastcgi-handler"></a>配置 FastCGI 处理程序

FastCGI 是在请求级别工作的接口。 IIS 接收传入的连接，并将每个请求转发到在一个或多个持久 Python 进程中运行的 WSGI 应用。 [Wfastcgi 包](https://pypi.io/project/wfastcgi)是使用每个 Python 站点扩展进行预安装和配置的，因此可通过在 web.config  中包含该代码轻松启用此包，正如下面针对基于 Bottle 框架的 Web 应用所示。 请注意，python.exe  和 wfastcgi.py  的完整路径位于 `PythonHandler` 键中：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <appSettings>
    <add key="PYTHONPATH" value="D:\home\site\wwwroot"/>
    <!-- The handler here is specific to Bottle; other frameworks vary. -->
    <add key="WSGI_HANDLER" value="app.wsgi_app()"/>
    <add key="WSGI_LOG" value="D:\home\LogFiles\wfastcgi.log"/>
  </appSettings>
  <system.webServer>
    <handlers>
      <add name="PythonHandler" path="*" verb="*" modules="FastCgiModule"
           scriptProcessor="D:\home\Python361x64\python.exe|D:\home\Python361x64\wfastcgi.py"
           resourceType="Unspecified" requireAccess="Script"/>
    </handlers>
  </system.webServer>
</configuration>
```

此处定义的 `<appSettings>` 可作为环境变量供应用使用：

- `PYTHONPATH` 的值可以自由扩展，但必须包括你的应用的根目录。
- `WSGI_HANDLER` 必须指向可从你的应用导入的 WSGI 应用。
- `WSGI_LOG` 为可选，但建议在调试应用时使用。

有关 Bottle、Flask 和 Django Web 应用的 web.config 内容的更多详细信息，请参阅[发布到 Azure](publishing-python-web-applications-to-azure-from-visual-studio.md)。

## <a name="install-packages"></a>安装包

通过站点扩展安装的 Python 解释器仅是 Python 环境的一部分。 可能还需要在该环境中安装不同的包。

若要直接在服务器环境中安装包，请使用以下方法之一：

| 方法 | 用法 |
| --- | --- |
| [Azure App Service Kudu 控制台](#azure-app-service-kudu-console) | 以交互方式安装包。 包必须为纯 Python，或必须发布系统。 |
| [Kudu REST API](#kudu-rest-api) | 可用于自动安装包。  包必须为纯 Python，或必须发布系统。 |
| 与应用捆绑 | 将包直接安装到项目中，然后将它们部署到应用服务，就如同它们是应用的一部分。 此方法可能是有效执行当前部署的最简单方法，具体取决于拥有的依赖项数量及其更新频率。 需要注意的是，这些库必须与服务器上的 Python 版本匹配，否则部署后会出现奇怪的错误。 也就是说，由于应用服务站点扩展中的 Python 版本与 python.org 上发布的版本完全相同，因此可以轻松获取兼容版本进行本地开发。 |
| 虚拟环境 | 不支持。 相反，应使用捆绑并将 `PYTHONPATH` 环境变量设置为指向包的位置。 |

### <a name="azure-app-service-kudu-console"></a>Azure App Service Kudu 控制台

使用 [Kudu 控制台](https://github.com/projectkudu/kudu/wiki/Kudu-console)可直接以提升的命令行访问应用服务服务器及其文件系统。 这是一个重要的调试工具，同时也支持 CLI 操作（如安装包）。

1. 选择“开发工具”   > “高级工具”  ，然后选择“转到”  ，从 Azure 门户上的“应用服务”页打开 Kudu。 此操作导航到与基应用服务 URL（插入的 `.scm` 除外）相同的 URL。 例如，如果基 URL 是 `https://vspython-test.azurewebsites.net/`，Kudu 则位于 `https://vspython-test.scm.azurewebsites.net/`（其中可以添加书签）：

    ![Azure App Service 的 Kudu 控制台](media/python-on-azure-console01.png)

1. 选择“调试控制台”   > “CMD”  ，打开控制台，在其中可导航到 Python 安装，并查看现已有哪些库。

1. 安装单个包：

    a. 导航到想在其中安装包的 Python 安装文件夹，如 d:\home\python361x64  。

    b. 使用 `python.exe -m pip install <package_name>` 安装包。

    ![示例：通过 Azure App Service 的 Kudu 控制台安装 bottle](media/python-on-azure-console02.png)

1. 如果已将应用的 requirements.txt  部署到服务器，请按如下方式安装所有这些要求：

    a. 导航到想在其中安装包的 Python 安装文件夹，如 d:\home\python361x64  。

    b. 运行 `python.exe -m pip install --upgrade -r d:\home\site\wwwroot\requirements.txt` 命令。

    建议使用 requirements.txt  ，因为这样可以轻松在本地和服务器上重新生成完全一样的包集。 只需记住在对 requirements.txt  进行任何更改后再访问控制台，然后再次运行该命令。

> [!Note]
> 应用服务上没有 C 编译器，因此需要为任何包含本机扩展模块的包安装该系统。 许多常用包本身附带滚轮。 对于不附带滚轮的包，请在本地开发计算机上使用 `pip wheel <package_name>`，然后将滚轮上传到站点。 有关示例，请参阅[使用 requirements.txt 管理所需的包](managing-required-packages-with-requirements-txt.md)。

### <a name="kudu-rest-api"></a>Kudu REST API

将命令发布到 `https://yoursite.scm.azurewebsites.net/api/command`，即可通过 Kudu REST API 远程运行命令，而无需通过 Azure 门户使用 Kudu 控制台。 例如，若要安装 `bottle` 包，则需将以下 JSON 发布到 `/api/command`：

```json
{
    "command": 'python.exe -m pip install bottle',
    "dir": '\home\python361x64'
}
```

有关命令和身份验证的信息，请参阅 [Kudu 文档](https://github.com/projectkudu/kudu/wiki/REST-API)。

还可通过 Azure CLI 使用 `az webapp deployment list-publishing-profiles` 命令查看凭据（请参阅 [az webapp deployment](/cli/azure/webapp/deployment?view=azure-cli-latest#az-webapp-deployment-list-publishing-profiles)（az webapp 部署））。 [GitHub](https://github.com/lmazuel/azure-webapp-publish/blob/master/azure_webapp_publish/kudu.py#L42) 上还提供用于发布 Kudu 命令的帮助程序库。
