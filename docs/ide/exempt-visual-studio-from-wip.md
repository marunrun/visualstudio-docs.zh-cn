---
title: 从 Windows 信息保护中免除
ms.date: 06/01/2018
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 714d85ea41674563922903f5bf38db04ffc2fbce
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978118"
---
# <a name="configure-visual-studio-as-a-wip-exempt-app"></a>将 Visual Studio 配置为 WIP 免除应用

[Windows 信息保护](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) 可帮助保护企业数据，避免数据从不受企业控制的电子邮件、社交媒体和公有云等应用泄露。 WIP 可帮助预防在企业拥有设备和个人设备上发生意外数据泄露，且无需更改环境或其他应用。

适用于 WIP 的启发式应用旨在防止企业数据进入不受保护的网络位置，以及避免对个人数据进行加密。 Visual Studio 不是启发式应用，因此不能在启用 WIP 的环境中使用，除非将其免除。 按照本文步骤启用 Visual Studio，使其在启用 WIP 的计算机上正常运行。

## <a name="configure-vs-as-a-wip-exempt-app"></a>将 VS 配置为 WIP 免除应用

可从 WIP 限制中免除 Visual Studio，但仍允许其使用企业数据。 WIP 免除应用可以使用 IP 地址或主机名连接到企业云资源。 无需应用任何加密，并且应用可以访问本地文件。

若要从 WIP 中免除 Visual Studio，请执行[免除桌面应用的步骤](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-intune-azure#exempt-apps-from-a-wip-policy)。

## <a name="create-a-wip-exempt-applocker-policy-file"></a>创建 WIP 免除 AppLocker 策略文件

由于 Visual Studio 包含多个二进制文件，因此需[创建 WIP 免除 AppLocker 策略文件](/windows/security/threat-protection/windows-defender-application-control/applocker/run-the-automatically-generate-rules-wizard)。 AppLocker 支持针对文件夹中的所有文件自动生成规则。

## <a name="add-appcompat-to-the-enterprise-cloud-resource-policy"></a>将 AppCompat 添加到企业云资源策略

若要指定 Visual Studio 可以在网络上访问的企业数据位置，请按照[定义受保护的应用可以在何处查找和发送企业数据的步骤](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-intune-azure#choose-where-apps-can-access-enterprise-data)执行操作。 若要防止 Windows 阻止通过 IP 地址连接到云资源，请确保在设置中添加 /AppCompat/ 字符串\*\*。

## <a name="see-also"></a>请参阅

- [使用 WIP 的应用的行为](/windows/security/information-protection/windows-information-protection/app-behavior-with-wip)