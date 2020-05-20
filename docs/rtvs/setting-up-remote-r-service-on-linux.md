---
title: 在 Linux 上设置远程 R 服务
description: 如何在 Ubuntu 和适用于 Linux 的 Windows 子系统上设置远程 R 服务。
ms.date: 12/04/2017
ms.topic: conceptual
author: kraigb
ms.author: kraigb
ms.reviewer: karthiknadig
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: c4d65388db0ef90f807ec85b8c9216d717c2b571
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62809552"
---
# <a name="remote-r-service-for-linux"></a>适用于 Linux 的远程 R 服务

适用于 Linux 的远程 R 服务当前打包为 rtvs-daemon。 Ubuntu 16.04、16.10 LTS 桌面、服务器和适用于 Linux 的 Windows 子系统（运行 Ubuntu）系统上支持守护程序，并在系统上对守护程序进行了测试。 本文的大量篇幅提供了在这些不同系统上设置远程 R 服务的说明。

配置远程计算机后，以下步骤将针对 Visual Studio 的 R 工具 (RTVS) 连接到该服务：

1. 选择“R 工具” > “窗口” > “工作区”，打开“工作区”窗。
1. 选择“添加连接”  。
1. 为连接命名并提供其 URL，例如 `https://localhost:5444`（适用于 Linux 的 Windows 子系统）或 `https://public-ip:5444`（Azure 容器）。 完成后，选择“保存”  。
1. 选择连接图标或双击连接项。
1. 提供登录凭据。 用户名的前缀必须为 `<<unix>>\`，如 `<<unix>>\ruser1`（所有与Linux 远程计算机的连接都有此要求）。
1. 如果在使用自签名证书，可能会看到一条警告。 该消息提供了更正警告的说明。

## <a name="set-up-remote-r-service"></a>设置远程 R 服务

本节介绍下列选项：

- [物理 Ubuntu 计算机](#physical-ubuntu-computer)
- [Ubuntu 服务器 VM 或 Azure 上的数据科学 VM](#ubuntu-server-vm-or-data-science-vm-on-azure)
- [本地或远程 Docker 容器（干净的生成）](#local-or-remote-docker-container-clean-build)
- [在 Azure 容器实例上运行的容器](#container-running-on-azure-container-instances)

在每种情况下，远程计算机上必须至少安装一个下列 R 解释器：

- [Microsoft R Open](https://mran.microsoft.com/open/)
- [CRAN R for Windows](https://cran.r-project.org/bin/linux/ubuntu/)

### <a name="physical-ubuntu-computer"></a>物理 Ubuntu 计算机

1. 登录计算机后，下载 rtvs-daemon tarball：

    ```bash
    wget -O rtvs-daemon.tar.gz https://aka.ms/r-remote-services-linux-binary-current
    tar -xvzf rtvs-daemon.tar.gz
    ```

1. 运行安装脚本：

    ```bash
    sudo ./rtvs-install
    ```

    要实现无提示自动化，请使用 `sudo ./rtvs-install -s`。

1. 启用并启动服务：

    ```bash
    sudo systemctl enable rtvsd
    sudo systemctl start rtvsd
    ```

1. 配置 SSL 证书（生产所需）。 默认情况下，rtvs-daemon 使用 `ssl-cert` 包生成的 `ssl-cert-snakeoil.pem` 和 `ssl-cert-snakeoil.pem`。 安装期间，它们合并为 `ssl-cert-snakeoil.pfx`。 如果要用于生产目的，请使用管理员提供的 SSL 证书。 可通过在 /etc/rtvs/rtvsd.config.json 中提供 .pfx 文件和可选导入密码配置 SSL 证书   。

1. （可选）检查服务正在运行：

    ```bash
    ps -A -f | grep rtvsd
    ```

    如果发现进程未在用户名 `rtvssvc` 下运行， 请使用以下命令启动它：

    ```bash
    sudo systemctl start rtvsd
    ```

1. 要进一步配置 rtvs-daemon，请参阅 `man rtvsd`。

### <a name="ubuntu-server-vm-or-data-science-vm-on-azure"></a>Ubuntu 服务器 VM 或 Azure 上的数据科学 VM

#### <a name="create-a-vm"></a>创建 VM

1. 登录 [Azure 门户](https://portal.azure.com)。
1. 导航到虚拟机，然后选择“添加”  。
1. 在可用 VM 映像列表中，搜索并选择以下选项之一：
    - Ubuntu 服务器：`Ubuntu Server 16.04 LTS`
    - 数据科学 VM：`Linux Data Science`（请参阅[数据科学虚拟机](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)了解详细信息）
1. 将部署模型设置为`Resource manager`，并选择“创建”  。
1. 为 VM 选择一个名字、提供用户名和密码（必须提供密码的，因为不支持 SSH 公钥登录）。
1. 对 VM 配置进行任何其他所需更改。
1. 选择 VM 大小，验证配置，然后选择“创建”  。 创建 VM 后，继续下一节。

#### <a name="configure-the-vm"></a>配置 VM

1. 在 VM 的“网络”部分中，将 5444 添加为允许的入站端口  。 要使用不同端口，请更改 RTVS 守护程序配置文件 (/etc/rtvs/rtvsd.config.json  ) 中的设置。
1. （可选）设置 DNS 名称，也可以使用 IP 地址。
1. 使用 SSH 客户端（如适用于 Windows 的 PuTTY）连接到 VM。
1. 按照上文[物理 Ubuntu 计算机](#physical-ubuntu-computer)中的说明操作。

### <a name="windows-subsystem-for-linux-wsl"></a>适用于 Linux 的 Windows 子系统 (WSL)

1. 按照 [Windows 10](/windows/wsl/install-win10#install-the-windows-subsystem-for-linux) 或 [Windows Server](/windows/wsl/install-on-server#enable-the-windows-subsystem-for-linux-wsl) 的 WSL 安装说明操作。
1. 在 Windows 上启动 bash，并按照之前[物理 Ubuntu 计算机](#physical-ubuntu-computer)中的说明操作，但其中一个步骤例外。 对于步骤 3，改用命令 `rtvsd` 启动服务，因为 WSL 当前不支持 systemd/systemctl 接口。

### <a name="local-or-remote-docker-container-clean-build"></a>本地或远程 Docker 容器（干净的生成）

1. 使用以下内容创建 Docker 文件，安装远程 R 服务守护程序和最新版本的 R。**注意**：此脚本创建名为“ruser1”、密码为“foobar”的用户，可在最后两个 `RUN` 语句中根据需要更改用户名和密码。

    ```docker
    FROM ubuntu:16.04

    ARG DEBIAN_FRONTEND=noninteractive

    RUN apt-get update \
     && apt-get install -y software-properties-common python-software-properties \
     && apt-get install -y apt-transport-https \
     && rm -rf /var/lib/apt/lists/*

    RUN sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' \
     && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893 \
     && sh -c 'echo "deb https://cran.revolutionanalytics.com/bin/linux/ubuntu xenial/" > /etc/apt/sources.list.d/cran-r.list' \
     && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9 \
     && rm -rf /var/lib/apt/lists/* \
     && apt-get clean

    RUN apt-get update --fix-missing && apt-get update \
     && apt-get install -y dotnet-dev-1.0.4 libexplain51 libzip4 libc6 git lshw ssl-cert wget \
     && rm -rf /var/lib/apt/lists/*

    # install R
    RUN apt-get update && apt-get install -y r-base-dev
    RUN apt upgrade -y

    # install rtvs-daemon
    RUN wget -O rtvs-daemon.tar.gz https://aka.ms/r-remote-services-linux-binary-current && tar -xvzf rtvs-daemon.tar.gz && ./rtvs-install -s

    RUN useradd --create-home ruser1
    RUN echo "ruser1:foobar" | chpasswd

    EXPOSE 5444
    ```

1. 生成并运行 Docker 文件：

    ```bash
    docker build -t myrimage .
    docker run -p 5444:5444 myrimage rtvsd
    ```

1. 要从 RTVS 连接到容器，请使用 `https://localhost:5444` 作为路径，并使用 `<<unix>>\ruser1` 作为用户名、`foobar` 作为密码。 如果容器在远程计算器上运行，则改用 `https://remote-host-name:5444` 作为路径。 可以通过更新 /etc/rtvs/rtvsd.config.json  来更改端口。

### <a name="container-running-on-azure-container-instances"></a>在 Azure 容器实例上运行的容器

1. 按照[本地或远程 Docker 容器（干净的生成）](#local-or-remote-docker-container-clean-build)中的说明创建映像。
1. 将容器推送到 Docker 中心或 Azure Container Repository。
1. 启动 Azure CLI 并使用 `az login` 命令登录。
1. 使用 `az container create` 命令创建容器，如果尚未将容器设置为将 `rtvsd` 作为 `systemd` 服务运行，则使用 `--command-line "rtvsd"`。 在以下命令中，映像应位于 Docker 中心。 还可以通过将 Container Repository 凭据参数添加到命令行来使用 Azure Container Repository。

    ```bash
    az container create --image myimage:latest --name myaz-container --resource-group myaz-container-res --ip-address public --port 5444 --cpu 2 --memory 4 --command-line "rtvsd"
    ```

1. 使用 `az container list` 命令检查状态。 查找 `provisioningState`：`Succeeded`。
1. 如果预配成功，则现在可以连接到容器。 在 `ipAddress` 字段中查找公共 IP 地址，此 IP 地址与 docker 文件中的凭据配合使用，可用于从 RTVS 连接到容器。
