---
ms.openlocfilehash: 8adac174fbc78778e7154a205088fb9e9a57ae4a
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "68143517"
---

1. 如果计算机上的 Visual Studio 中打开有 ASP.NET 项目，则在该计算机的解决方案资源管理器中右键单击该项目，然后选择“发布”。

1. 如果先前配置了任何发布配置文件，则“发布”窗格会显示。 点击“新建配置文件”。

1. 在“选取发布目标”对话框中，点击“导入配置文件”。

    ![选择发布](../../deployment/media/tutorial-publish-tool-import-profile.png)

1. 导航到上一节中创建的发布设置文件的位置。

1. 在“导入发布设置文件”对话框中，导航到并选择在上一节中创建的配置文件，然后单击“打开”。

    Visual Studio 开始执行部署过程，并且输出窗口将显示进度和结果。

    如果出现任何部署错误，请单击“设置”以编辑设置。 修改设置，然后单击“验证”以测试新设置。 如果找不到主机名，请尝试“服务器”和“目标 URL”字段中的 IP 地址而不是主机名。

    ![编辑发布工具中的设置](../../deployment/media/tutorial-configure-publish-settings-in-tool.png)
