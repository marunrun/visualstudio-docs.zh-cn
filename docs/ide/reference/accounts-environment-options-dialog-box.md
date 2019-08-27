---
title: 帐户选项参考
ms.date: 12/10/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.RoamingSettings
ms.assetid: 3cfe09d2-1120-46e8-b882-f7056acb778b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cc3d88fd07ec5d345b3e8697ef69b193ece0fac1
ms.sourcegitcommit: ce1ab8a25c66a83e60eab80ed8e1596fe66dd85c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2019
ms.locfileid: "68604898"
---
# <a name="accounts-environment-options-dialog-box"></a>“帐户”、“环境”、“选项”对话框

使用此页面设置与用于登录 Visual Studio 的帐户相关的各种选项。

## <a name="personalization-account"></a>个性化帐户

### <a name="synchronize-settings-across-devices"></a>跨设备同步设置

此选项用于指定是否跨多台计算机同步设置。 有关详细信息，请参阅[同步设置](../../ide/synchronized-settings-in-visual-studio.md)。

### <a name="enable-device-code-flow"></a>启用设备代码流

选中此选项后，当在“文件” > “帐户设置”页上选择“添加帐户”时，Visual Studio 的行为将发生变化    。 会改为显示对话框，而不是“登录到帐户”页面，该对话框提供 URL 和代码，用于粘贴到 Web 浏览器中进行登录  。 如果不能以常规方式登录到 Visual Studio（例如，如果使用的是较低版本的 Internet Explorer，或者防火墙限制访问），这个选项会非常有用。 有关详细信息，请参阅[使用多个用户帐户](../work-with-multiple-user-accounts.md#add-an-account-using-device-code-flow)。

## <a name="registered-azure-clouds"></a>注册的 Azure 云

本部分展示可通过一个或多个帐户（用于登录 Visual Studio）访问的 Azure 云实例。 例如，可以访问公司数据中心中的 Azure 专用实例。 或者，可以访问 Azure 的主权或政府实例，比如 Azure 中国世纪互联或 Azure 美国。政府。 列表中默认显示全局 Azure 云实例，并且无法删除。

通过选择“添加”按钮，可注册额外的 Azure 云  。 “添加新的 Azure 云”对话框列出了几个可以连接到的、众所周知的 Azure 云实例，或者可以输入专用 Azure 终结点的 URL  。

![添加新的 Azure 云实例](media/add-new-azure-cloud.png)

注册额外的 Azure 云之后，可以选择登录 Visual Studio 时要登录的 Azure 云。

## <a name="see-also"></a>请参阅

- [跨多台计算机同步设置](../synchronized-settings-in-visual-studio.md)
- [登录 Visual Studio](../signing-in-to-visual-studio.md)
- [使用多个用户帐户](../work-with-multiple-user-accounts.md)
- [环境设置](../environment-settings.md)