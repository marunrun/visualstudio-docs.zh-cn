---
title: 为 Python Web 应用配置 IIS
description: 如何将 Python Web 应用配置为使用 Windows 虚拟机中的 Internet Information Services 运行。
ms.date: 12/06/2018
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: 551cff18849f0e8ad9fcd6f2c1e08561291b177f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62957367"
---
# <a name="configure-python-web-apps-for-iis"></a>为 Python Web 应用配置 IIS

如果将 Internet Information Services (IIS) 用作 Windows 计算机（包括 [Azure 上的 Windows 虚拟机](/azure/architecture/reference-architectures/n-tier/windows-vm)）中的 Web 服务器，必须在 Python 应用的 web.config  文件中添加特定设置，这样 IIS 才能正确处理 Python 代码。 计算机自身也必须安装 Python，以及 Web 应用需要的任何包。

> [!Note]
> 本文之前介绍了如何对 Windows 上的 Azure 应用服务配置 Python。 此方案使用的 Python 扩展和 Windows 主机已遭弃用，改用 Linux 上的 Azure 应用服务。 有关详细信息，请参阅[将 Python 应用发布到 Azure 应用服务 (Linux)](publishing-python-web-applications-to-azure-from-visual-studio.md)。 不过，仍可从[管理 Windows 上包含 Python 扩展的应用服务](managing-python-on-azure-app-service.md)中获取旧文章。

## <a name="install-python-on-windows"></a>在 Windows 上安装 Python

若要运行 Web 应用，请先直接在 Windows 主机上安装相应版本的 Python，如[安装 Python 解释器](installing-python-interpreters.md)中所述。

记录 `python.exe` 解释器的位置，后续步骤中将会用到此位置。 为方便起见，可以将此位置添加到 PATH 环境变量中。

## <a name="install-packages"></a>安装包

使用专用主机时，可使用全局 Python 环境（而不是虚拟环境）运行应用。 相应地，只需在命令提示符处运行 `pip install -r requirements.txt`，即可将应用的所有要求都安装到全局环境中。

## <a name="set-webconfig-to-point-to-the-python-interpreter"></a>将 web.config 设置为指向 Python 解释器

应用的 web.config 文件指示 Windows 上运行的 IIS (7+) Web 服务器，应如何通过 HttpPlatform（推荐）或 FastCGI 处理 Python 请求  。 Visual Studio 2015 及更早版本会自动进行这些修改。 使用 Visual Studio 2017 及更高版本时，必须手动修改 web.config  。

### <a name="configure-the-httpplatform-handler"></a>配置 HttpPlatform 处理程序

HttpPlatform 模块将套接字连接直接传递到独立的 Python 进程。 借助此传递可根据需要运行任何 Web 服务器，但需要用于运行本地 Web 服务器的启动脚本。 在 web.config  的 `<httpPlatform>` 元素中指定脚本，其中 `processPath` 属性指向站点扩展的 Python 解释器，`arguments` 属性指向脚本和希望提供的任何参数：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="PythonHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified"/>
    </handlers>
    <httpPlatform processPath="c:\python36-32\python.exe"
                  arguments="c:\home\site\wwwroot\runserver.py --port %HTTP_PLATFORM_PORT%"
                  stdoutLogEnabled="true"
                  stdoutLogFile="c:\home\LogFiles\python.log"
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

FastCGI 是在请求级别工作的接口。 IIS 接收传入的连接，并将每个请求转发到在一个或多个持久 Python 进程中运行的 WSGI 应用。

若要使用 wfastcgi 包，请先安装并配置它，如 [pypi.org/project/wfastcgi/](https://pypi.io/project/wfastcgi) 所述。

接下来，将应用的 web.config  文件修改为，在 `PythonHandler` 键中添加 python.exe  和 wfastcgi.py  的完整路径。 若要执行下列步骤，需要已在 c:\python36-32  中安装 Python，且应用代码位于 c:\home\site\wwwroot  中；请根据自己的路径进行相应调整：

1. 修改 web.config  中的 `PythonHandler` 条目，让路径与 Python 安装位置一致（有关确切的详细信息，请参阅 [IIS 配置参考](https://www.iis.net/configreference) (iis.net)）。

    ```xml
    <system.webServer>
      <handlers>
        <add name="PythonHandler" path="*" verb="*" modules="FastCgiModule"
            scriptProcessor="c:\python36-32\python.exe|c:\python36-32\wfastcgi.py"
            resourceType="Unspecified" requireAccess="Script"/>
      </handlers>
    </system.webServer>
    ```

1. 在 web.config  的 `<appSettings>` 部分中，为 `WSGI_HANDLER`、`WSGI_LOG`（可选）和 `PYTHONPATH` 添加键：

    ```xml
    <appSettings>
      <add key="PYTHONPATH" value="c:\home\site\wwwroot"/>
      <!-- The handler here is specific to Bottle; see the next section. -->
      <add key="WSGI_HANDLER" value="app.wsgi_app()"/>
      <add key="WSGI_LOG" value="c:\home\LogFiles\wfastcgi.log"/>
    </appSettings>
    ```

    应用可以将这些 `<appSettings>` 值用作环境变量：

    - `PYTHONPATH` 的值可以自由扩展，但必须包括你的应用的根目录。
    - `WSGI_HANDLER` 必须指向可从你的应用导入的 WSGI 应用。
    - `WSGI_LOG` 为可选，但建议在调试应用时使用。

1. 设置 web.config  中的 `WSGI_HANDLER` 条目，以适合正在使用的框架：

    - **Bottle**：确保 `app.wsgi_app` 后面有括号，如下所示。 此操作是必需的，因为该对象是函数（请参阅 app.py  )）而非变量：

        ```xml
        <!-- Bottle apps only -->
        <add key="WSGI_HANDLER" value="app.wsgi_app()"/>
        ```

    - **Flask**：将 `WSGI_HANDLER` 值更改为 `<project_name>.app`，其中 `<project_name>` 与项目名称匹配。 可通过查看 runserver.py  中的 `from <project_name> import app` 语句，找到准确的标识符。 例如，如果项目命名为“FlaskAzurePublishExample”，则该条目如下所示：

        ```xml
        <!-- Flask apps only: change the project name to match your app -->
        <add key="WSGI_HANDLER" value="flask_iis_example.app"/>
        ```

    - **Django**：对于 Django 项目，需要对“web.config”进行两项更改  。 首先，将 `WSGI_HANDLER` 值更改为 `django.core.wsgi.get_wsgi_application()`（该对象位于 wsgi.py  文件中）：

        ```xml
        <!-- Django apps only -->
        <add key="WSGI_HANDLER" value="django.core.wsgi.get_wsgi_application()"/>
        ```

        其次，在 `WSGI_HANDLER` 条目下添加以下条目，并将 `DjangoAzurePublishExample` 替换为项目名称：

        ```xml
        <add key="DJANGO_SETTINGS_MODULE" value="django_iis_example.settings" />
        ```

1. **仅限 Django 应用**：在 Django 项目的“settings.py”文件中，将网站 URL 域或 IP 地址添加到 `ALLOWED_HOSTS` 中，如下所示（当然要将“1.2.3.4”替换为你自己的 URL 或 IP 地址）  ：

    ```python
    # Change the URL or IP address to your specific site
    ALLOWED_HOSTS = ['1.2.3.4']
    ```

    未能将 URL 添加到该阵列会导致出现错误“不允许的主机 / 无效的 HTTP_HOST 标头: ‘\<站点 URL\>’。  可能需要将‘\<站点 URL\>’添加到 ALLOWED_HOSTS。

    请注意，当数组为空时，Django 会自动允许“localhost”和“127.0.0.1”，而添加生产 URL 则会删除这些功能。 因此，可能需要保留单独的 settings.py  开发和生产副本，或者使用环境变量来控制运行时值。

## <a name="deploy-to-iis-or-a-windows-vm"></a>部署到 IIS 或 Windows VM

如果项目已包含正确的 web.config  文件，便可使用“解决方案资源管理器”  中项目快捷菜单内的“发布”  命令，并选择“IIS、FTP 等”  选项，从而将项目发布到运行 IIS 的计算机。 在这种情况下，Visual Studio 仅将项目文件复制到服务器；你要负责所有服务器端配置。
