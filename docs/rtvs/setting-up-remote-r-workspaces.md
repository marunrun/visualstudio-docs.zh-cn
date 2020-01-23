---
title: 远程 R 工作区
description: 如何设置远程 R 工作区并从 Visual Studio 连接到该工作区。
ms.date: 12/04/2017
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 686f98aaaade035f1632139d255ccff8b37eddf3
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850058"
---
# <a name="set-up-remote-workspaces"></a>设置远程工作区

本文说明如何为远程服务器配置 SSL 和相应的 R 服务。 这使针对 Visual Studio 的 R 工具 (RTVS) 可以连接到该服务器上的远程工作区。

## <a name="remote-computer-requirements"></a>远程计算机要求

- Windows 10、Windows Server 2016 或 Windows Server 2012 R2。 RTVS 同时还要求
- [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) 或更高版本

## <a name="install-an-ssl-certificate"></a>安装 SSL 证书

RTVS 要求通过 HTTP 实现所有与远程服务器的通信，这就要求服务器上必须有 SSL 证书。 可以使用受信任证书颁发机构签名的证书（推荐），或自签名证书。 （自签名证书会导致 RTVS 在连接时发出警告。）无论使用哪种证书，都需要将其安装在计算机上，并允许访问它的私钥。

### <a name="obtain-a-trusted-certificate"></a>获取受信任的证书

受信任的证书由证书颁发机构颁发（有关背景知识，请参阅[维基百科中的证书颁发机构](https://en.wikipedia.org/wiki/Certificate_authority)）。 和获取政府颁发的身份证类似，受信任证书的颁发过程更繁琐且可能需要付费，但还是要验证请求和请求者的真实性。

证书中要求的键字段是 R 服务器计算机的完全限定域名。 证书颁发机构会要求提供证据，证明你有权为服务器所属的域创建新服务器。

有关详细背景信息，请参阅维基百科中的[公钥证书](https://en.wikipedia.org/wiki/Public_key_certificate)。

## <a name="install-an-ssl-certificate-on-windows"></a>在 Windows 上安装 SSL 证书

必须在 Windows 上手动安装 SSL 证书。 请按照以下说明安装 SSL 证书。

### <a name="obtain-a-self-signed-certificate-windows"></a>获取自签名证书 (Windows)

如有可信证书，则跳过此部分。 和来自受信任证书颁发机构的证书相比，自签名证书更像是为自己创建一张身份证。 当然，比起使用受信任的颁发机构，此过程要简便许多，但是同样缺少强身份验证。这意味着攻击者可将自己的证书替换为未签名的证书，捕获客户端和服务器之间的所有流量。 因此，仅可在测试方案和受信任的网络中使用自签名证书，而不应在生产中使用它  。

为此，在使用自签名证书连接服务器时，RTVS 总会发出下列警告：

![自签名证书警告对话框](media/workspaces-remote-self-signed-certificate-warning.png)

颁发自签名证书：

1. 使用 Administrator 帐户登录到 R 服务器计算机。
1. 打开一个新的管理员 PowerShell 命令提示符，发布下列命令，将 `"remote-machine-name"` 替换为服务器计算机的完全限定域名。

    ```ps
    New-SelfSignedCertificate -CertStoreLocation Cert:\LocalMachine\My -DnsName "remote-machine-name"
    ```

1. 如果此前从未在 R 服务器计算机上运行过 PowerShell，则运行下列命令显式启用运行命令：

    ```ps
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
    ```

有关背景信息，请参阅维基百科中的[自签名证书](https://en.wikipedia.org/wiki/Self-signed_certificate)。

### <a name="install-the-certificate"></a>安装证书

要在远程计算机上安装证书，请从自命令提示符运行 certlm.msc（证书管理器）  。 右键单击“个人”文件夹，选择“所有任务” > “导入”命令    ：

![导入证书命令](media/workspaces-remote-certificate-import.png)

### <a name="grant-permissions-to-read-the-ssl-certificates-private-key"></a>授予读取 SSL 证书私钥的权限

导入证书后，即授予 `NETWORK SERVICE` 帐户读取私钥的权限，如下面的说明所述。 `NETWORK_SERVICE` 是用于运行 R 服务代理的帐户，也是终止服务器计算机的入站 SSL 连接的服务。

1. 从管理员命令提示符运行 certlm.msc（证书管理器）  。
1. 展开“个人” > “证书”，右键单击证书，然后选择“所有任务” > “管理私钥”     。
1. 邮件单击证书，在“所有任务”下选择“管理私钥”命令   。
1. 在出现的对话框中选择“添加”  ，然后输入 `NETWORK SERVICE` 作为帐户名：

    ![管理私钥对话框，添加 NETWORK_SERVICE](media/workspaces-remote-manage-private-key-dialog.png)

1. 连续选择“确定”  两次以消除对话框，并提交更改。

## <a name="install-an-ssl-certificate-on-ubuntu"></a>在 Ubuntu 上安装 SSL 证书

`rtvs-daemon` 程序包将在安装过程中默认安装自签名证书。

### <a name="obtain-a-self-signed-certificate-ubuntu"></a>获取自签名证书 (Ubuntu)

有关使用自签名证书的好处和风险，请参阅 Windows 说明。 `rtvs-daemon` 包在安装期间会生成并配置自签名证书。 仅在需要替换自动生成的自签名证书时，才需执行此操作。

若要自行颁发自签名证书，请执行以下操作：

1. 使用 SSH 连接到或登录到 Linux 计算机。
2. 安装 `ssl-cert` 程序包：

    ```sh
    sudo apt-get install ssl-cert
    ```

3. 运行 `make-ssl-cert` 以生成默认的自签名 SSL 证书：

    ```sh
    sudo make-ssl-cert generate-default-snakeoil --force-overwrite
    ```

4. 将生成的密钥和 PEM 文件转换为 PFX。 生成的 PFX 应位于主文件夹中：

    ```sh
    openssl pkcs12 -export -out ~/ssl-cert-snakeoil.pfx -inkey /etc/ssl/private/ssl-cert-snakeoil.key -in /etc/ssl/certs/ssl-cert-snakeoil.pem -password pass:SnakeOil
    ```

### <a name="configure-rtvs-daemon"></a>配置 RTVS 守护程序

必须在 /etc/rtvs/rtvsd.config.json 中设置 SSL 证书文件路径（PFX 路径）  。 分别使用文件路径和密码更新 `X509CertificateFile` 和 `X509CertificatePassword`。

```json
{
  "logging": { "logFolder": "/tmp" },
  "security": {
    "allowedGroup": "",
    "X509CertificateFile": "/etc/rtvs/ssl-cert-snakeoil.pfx",
    "X509CertificatePassword": "SnakeOil"
  },
  "startup": { "name": "rtvsd" },
  "urls": "https://0.0.0.0:5444"
}
```

保存该文件并重新启动守护程序 (`sudo systemctl restart rtvsd`)。

## <a name="install-r-services-on-windows"></a>在 Windows 上安装 R 服务

要运行 R 代码，远程计算机必须安装 R 解释器，如下所示：

1. 下载并安装下列内容之一：

   - [Microsoft R Open](https://mran.microsoft.com/open/)
   - [CRAN R for Windows](https://cran.r-project.org/bin/windows/base/)

     虽然二者功能相同，但 Microsoft R Open 另外还受益于 [Intel Math Kernel 库](https://software.intel.com/intel-mkl)的附加硬件加速线性代数库。

2. 运行 [R 服务安装程序](https://github.com/Microsoft/RTVS/blob/master/doc/rtvsd/rtvs-remote-downloads.md)并根据提示重启。 安装程序执行如下操作：

    - 在 %PROGRAMFILES%\R Tools for Visual Studio\1.0\\ 中创建文件夹并复制所有所需二进制文件  。
    - 安装 `RHostBrokerService` 和 `RUserProfileService` 并配置为自动启动。
    - 将 `seclogon` 服务配置为自动启动。
    - 将 Microsoft.R.Host.exe 和 Microsoft.R.Host.Broker.exe 添加到默认端口 5444 上的防火墙入站规则   。

重启计算机时，R 服务会自动启动：

- R 主机代理服务处理 Visual Studio 和计算机上 R 代码运行的进程之间的所有 HTTPS 流量  。
- R 用户配置文件服务  是处理 Windows 用户配置文件创建的特权组件。 新用户首次登陆 R 服务器计算机时调用该服务。

在服务管理控制台 (compmgmt.msc) 中可以看到这些服务  。

## <a name="install-r-services-on-linux"></a>在 Linux 上安装 R 服务

要运行 R 代码，远程计算机必须安装 R 解释器，如下所示：

1. 下载并安装下列内容之一：

   - [Microsoft R Open](https://mran.microsoft.com/open/)
   - [CRAN R for Windows](https://cran.r-project.org/bin/linux/ubuntu/)

     虽然二者功能相同，但 Microsoft R Open 另外还受益于 [Intel Math Kernel 库](https://software.intel.com/intel-mkl)的附加硬件加速线性代数库。

2. 请按照有关[适用于 Linux 的远程 R 服务](setting-up-remote-r-service-on-linux.md)的说明进行操作，该服务涵盖了物理 Ubuntu 计算机、Azure Ubuntu VM、适用于 Linux 的 Windows 子系统 (WSL) 和 Docker 容器（包括在 Azure 容器存储库上运行的那些容器）。

## <a name="configure-r-services"></a>配置 R 服务

当在远程计算机上运行 R 服务时，还需创建用户帐户、设置防火墙规则、配置 Azure 网络和配置 SSL 证书。

1. 用户帐户：为每个要访问远程计算机的用户创建帐户。 可创建标准（非特权）本地用户帐户，也可将 R 服务器计算机加入到域，并将相应的安全组添加到 `Users` 安全组。

1. 防火墙规则：默认情况下，`R Host Broker` 侦听 TCP 端口 5444。 因此，请确保已同时为入站和出站流量启用 Windows 防火墙规则（对于安装包和类似的方案，出站是必需的）。  R 服务安装程序为内置的 Windows 防火墙自动设置这些规则。 但是，如果正在使用第三方防火墙，则需手动为 `R Host Broker` 开启端口 5444。

1. Azure 配置：如果远程计算机是 Azure 上的虚拟机，则也会为 Azure 网络内的入站流量开启端口 5444，使其不受 Windows 防火墙影响。 有关详细信息，请参阅 Azure 文档中的[使用网络安全组筛选网络流量](/azure/virtual-network/virtual-networks-nsg)。

1. 告知 R 主机代理要加载的 SSL 证书：如果要在 Intranet 服务器上安装证书，则服务器的完全限定域名可能与其 NETBIOS 名称相同。 在这种情况下，无需进行任何操作，因为加载的是默认证书。

    但是，如果正在面向 Internet 的服务器（如 Azure VM）上安装证书，请使用服务器的完全限定域名 (FQDN)，这是因为面向 Internet 的服务器的 FQDN 不可能与其 NETBIOS 名称相同。

    若要使用 FQDN，请导航到安装了 R Services 的位置（默认为 %PROGRAM FILES%\R Remote Service for Visual Studio\1.0），在文本编辑器中打开 Microsoft.R.Host.Broker.Config.json 文件，然后将其内容替换为以下内容，将 CN 分配到服务器的 FQDN，例如 `foo.westus.cloudapp.azure.com`   ：

    ```json
    {
      "server.urls": "https://0.0.0.0:5444",
      "security": {
        "X509CertificateName": "CN=your-server-fully-qualified-domain-name"
      }
    }
    ```

    保存文件，重启计算机以应用更改。

## <a name="troubleshooting"></a>疑难解答

**问：R 服务器计算机没有响应该怎么办？**

尝试从命令行对远程计算机执行 ping 操作： `ping remote-machine-name`。 如果 ping 操作失败，请确保计算机正在运行。

**问：R 交互窗口显示远程计算机已启动，为什么服务无法运行？**

有三个可能的原因：

- 未在计算机上安装 [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) 或更高版本。
- 未同时为端口 5444 上的入站和出站连接启用 `Microsoft.R.Host.Broker` 和 `Microsoft.R.Host` 的防火墙规则。
- 未安装具有 `CN=<remote-machine-name>` 的 SSL 证书。

执行上述更改后，重启计算机。 然后，确保 `RHostBrokerService` 和 `RUserProfileService` 通过任务管理器（服务选项卡）或 services.msc 运行  。

**问：为什么连接到 R 服务器后，R 交互窗口显示“401 拒绝访问”？**

可能有两种原因：

- 一种很有可能的情况是 `NETWORK SERVICE` 帐户不具有对 SSL 证书私钥的访问权限。 请根据前面的指南，授予 `NETWORK SERVICE` 对私钥的访问权限。
- 请确保 `seclogon` 服务正在运行。 使用 services.msc 配置 `seclogon` 以自动开始  。

**问：为什么连接到 R 服务器后，R 交互窗口显示“404 未找到”？**

此错误可能是由于缺少 Visual C++ 可再发行库产生的。 检查 R 交互窗口，查看是否有关于缺少库 (DLL) 的消息。 然后检查是否已安装 VS 2015 可再发行组件和 R。

**问：无法从 R 交互窗口访问 Internet/资源，我该怎么办？**

请确保 `Microsoft.R.Host.Broker` 和 `Microsoft.R.Host` 的防火墙规则允许端口 5444 上的出站访问。 应用更改后，重启计算机。

**问：我已尝试上述解决方案，但仍不起作用。现在该怎么办？**

在 C:\Windows\ServiceProfiles\NetworkService\AppData\Local\Temp 中查找日志文件  。对于运行的 R 代理服务的每个实例，此文件夹都有一个单独的日志文件。 每当服务重启时，都会创建新的日志文件。 检查最新的日志文件，查找有关可能发生哪些错误的线索。
