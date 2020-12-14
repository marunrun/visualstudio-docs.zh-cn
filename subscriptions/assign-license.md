---
title: 将 Visual Studio 订阅分配给用户 | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 4e529a43-7aed-4eee-895d-862a631952df
ms.date: 09/21/2020
ms.topic: conceptual
description: 了解管理员如何将许可证分配给订阅者
ms.openlocfilehash: dd80a14a3ff57100f210fd7ae1b882c0ab7a9faf
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915409"
---
# <a name="assign-licenses-in-the-visual-studio-subscriptions-administration-portal"></a>在 Visual Studio 订阅管理门户中分配许可证
作为 Visual Studio 订阅管理员，你可以使用管理门户为个人用户和用户组分配订阅。

对于用户组，你可以选择分配订阅的方式。  
- 可以一次分配一个订阅。
- 也可以使用 [批量添加](assign-license-bulk.md)功能快速轻松地上传订阅者列表及其订阅信息。
- 如果你的组织使用 Microsoft Azure Active Directory (Azure AD)，则可以[使用 Azure AD 组将订阅分配给用户组](./assign-license-bulk.md#use-azure-active-directory-groups-to-assign-subscriptions)。  


## <a name="add-a-single-subscriber"></a>添加单个订阅者
观看视频或继续阅读，了解如何为新用户分配 Visual Studio 订阅，以便他们可以访问订阅权益。

<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4vpPh]


1. 登录到[管理门户](https://manage.visualstudio.com)。
2. 要为单个 Visual Studio 订阅者分配许可证，请在表的顶部选择“添加”，然后选择“单个订阅者”。
   > [!div class="mx-imgBorder"]
   > ![添加单个订阅者](_img/assign-license-add/add-subscriber-individual.png "选择“添加”，然后选择要分配单个订阅的单个订阅者。")
3. 在表单域中输入新订阅者的信息。 如果你的组织使用 Azure Active Directory，则“姓名”字段可充当搜索功能，用于查找当前目录中的用户，以便从搜索结果中选择正确的用户。 当你选择该用户后，系统会自动填充登录电子邮件和通知电子邮件。  如果在组织中找不到该订阅者，通知电子邮件将不会自动填充，但你可以手动添加其他电子邮件地址，并向其发送与订阅相关的电子邮件。  如果电子邮件服务阻止传入电子邮件发送到登录电子邮件地址，请务必指定其他通知电子邮件地址，以便订阅者和管理员接收来自 Microsoft 的与订阅相关的重要电子邮件。
   > [!div class="mx-imgBorder"]
   > ![订阅者详细信息](_img/assign-license-add/subscriber-details.png "输入订阅者名称和其他详细信息，或从租户成员中进行选择。")

    > [!NOTE]
    > 为了在你输入订阅者姓名时显示 Azure Active Directory 租户的成员，管理员必须是该租户的成员。 


    如果希望此订阅者在登录 [Visual Studio 订阅门户](https://my.visualstudio.com?wt.mc_id=o~msft~docs)时可以访问软件下载，请务必将“下载设置”部分中的下载切换保持启用状态。 如果选择禁用下载，则用户将无法访问软件下载。  还将禁用对产品密钥的访问权限。  订阅者仍可访问订阅中包含的所有其他权益。
   > [!div class="mx-imgBorder"]
   > ![下载的访问权限](media/access-to-downloads.png "选择“允许”，为订阅者提供对软件下载的访问权限。")

    如果要向订阅添加自己的引用说明，则可以在“添加引用”部分执行操作。
   > [!div class="mx-imgBorder"]
   > ![向每个订阅添加自己的引用说明](media/add-subscriber-reference-notes.png "使用“引用”字段记录有关此订阅的任何注释。")

    完成选择选项和输入订阅者数据后，选择“添加订阅者”弹出窗口底部的“添加” 。
   > [!div class="mx-imgBorder"]
   > ![选择“添加”按钮](media/add-button.png "选择“添加”以保存信息并将订阅分配给订阅者。")

## <a name="why-use-a-different-notification-email-address"></a>为什么要使用其他通知电子邮件地址？
某些组织将电子邮件服务设置为阻止来自其他域的传入电子邮件。  阻止传入电子邮件意味着订阅者和管理员会错过重要资讯：
- 订阅者将不会收到有关已向其分配的订阅的通知。  这也会妨碍他们激活一些附带的权益。  
- 分配到具有 GitHub Enterprise 的 Visual Studio 订阅的订阅者将不会收到加入 GitHub 组织的邀请，这意味着他们将无法接受邀请。 他们必须接受通过电子邮件发送的邀请才能获得对 GitHub 组织的访问权限。 
- 将管理员添加到协议时，这些管理员不会受到通知，他们也不会收到每月管理员报表或功能更改通知，这会影响他们管理订阅的方式。

通过使用通知电子邮件地址，订阅者可以接收有关其订阅的重要通信，而无需更改其登录电子邮件地址的功能。  

## <a name="resend-assignment-emails"></a>重新发送分配电子邮件
添加订阅者后，系统会向新订阅者自动发送一封分配电子邮件，为其提供进一步说明。 通过选中订阅者，然后选择顶部菜单中的“重新发送”按钮，可以随时再次发送分配电子邮件。  若要向多个用户重新发送电子邮件，请在选择订阅者时按住 Ctrl 键。  选择“重新发送”按钮后，会看到一个对话框，要求确认是否要向这些订阅者重新发送。  



## <a name="see-also"></a>请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)


## <a name="next-steps"></a>后续步骤
- 有很多用户要添加？  了解如何将订阅分配给[多个订阅者](assign-license-bulk.md)。
- 需要帮助？  联系 [Visual Studio 管理和订阅支持](https://visualstudio.microsoft.com/support/support-overview-vs)。