---
ms.openlocfilehash: 69f4f4c2b55670d510652b44a203b9f0eafcc53a
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "68143547"
---

1. 关闭并重新打开 IIS 管理控制台以在 UI 中显示更新的配置选项。

2. 在 IIS 中，右键单击“默认网站”，选择“部署” > “配置 Web 部署发布”    。

    ![配置 Web 部署配置](../../deployment/media/tutorial-configure-web-deploy-publishing.png)

3. 在“配置 Web 部署发布”对话框中，检查设置  。

4. 单击“设置”  。

    在“结果”面板中，输出显示已为指定用户授予访问权限，并且已在对话框中显示的位置生成了具有 .publishsettings 文件扩展名的文件   。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <publishData>
      <publishProfile
        publishUrl="https://myhostname:8172/msdeploy.axd"
        msdeploySite="Default Web Site"
        destinationAppUrl="http://myhostname:80/"
        mySQLDBConnectionString=""
        SQLServerDBConnectionString=""
        profileName="Default Settings"
        publishMethod="MSDeploy"
        userName="myhostname\myusername" />
    </publishData>
    ```

    根据 Windows Server 和 IIS 配置，可以在 XML 文件看到不同的值。 下面是有关所看到的值的一些详细信息：

   * `publishUrl` 属性中引用的 msdeploy.axd 文件是 Web 部署动态生成的 HTTP 处理程序文件  。 （用于测试目的，`http://myhostname:8172` 通常也适用。）
   * `publishUrl` 端口设置为端口 8172，这是 Web 部署的默认端口。
   * `destinationAppUrl` 端口设置为端口 80，这是 IIS 部署的默认端口。
   * 如果使用主机名无法在 Visual Studio 中连接到远程主机（在后续步骤中），请测试 IP 地址以代替主机名。

     > [!NOTE]
     > 如果要发布到在 Azure VM 上运行的 IIS，则必须在网络安全组中打开 Web 部署和 IIS 端口。 有关详细信息，请参阅[安装和运行 IIS](/azure/virtual-machines/windows/quick-create-portal#install-web-server)。

5. 将此文件复制到运行 Visual Studio 的计算机上。
