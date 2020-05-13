---
title: 客户体验改善计划
description: 了解如何在 Visual Studio 中管理隐私设置。
ms.date: 05/21/2018
ms.topic: conceptual
author: PoulChapman
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b6c785b755b64f0dd7e367a01d9c05c1981ea558
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "71693015"
---
# <a name="visual-studio-customer-experience-improvement-program"></a>Visual Studio 客户体验改善计划

Visual Studio 客户体验改善计划 (VSCEIP) 旨在随着时间推移帮助 Microsoft 改进 Visual Studio。 此程序[收集有关错误的信息](../ide/diagnostic-data-collection.md)、计算机硬件以及 Visual Studio 的使用方式，而不中断用户在计算机中的任务。 收集的信息帮助 Microsoft 确定要改善的功能。 本文档介绍如何选择加入或退出 VSCEIP。

[!INCLUDE [gdpr-hybrid-note](../misc/includes/gdpr-hybrid-note.md)]
> [!NOTE]
> VSCEIP 遥测选择加入或退出设置不适用于 Visual Studio 中的“报告问题”。 报告问题时，仅当你通过单击“提交”提供权限时，才会收集日志并发送给 Microsoft。 如果你有兴趣在提交到“报告问题”之前管理日志，请参阅[反馈数据隐私](./developer-community-privacy.md)了解更多详细信息。

## <a name="opt-in-or-out"></a>选择加入或退出

VSCEIP 默认开启。 可以按照以下步骤将其关闭或者再次打开：

1. 在 Visual Studio 中，选择“帮助”   > “发送反馈”  ，然后选择“设置”  。

   “Visual Studio 体验改善计划”对话框随即打开  。

1. 若要选择退出，请选择“否，我不想参加”，然后选择“确定”   。 若要选择加入，请选择“是，我愿意参加”，然后选择“确定”   。

   ![“Visual Studio 体验改善计划”对话框](media/experience-improvement-program.png)

### <a name="registry-settings"></a>注册表设置

如果安装 [Visual Studio 生成工具](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2017)，必须更新注册表来配置 VSCEIP。 企业客户可以设置基于注册表的策略，利用这种方式构造选择加入或不加入 VSCEIP 的组策略。

相关注册表项和设置如下所示：

::: moniker range="vs-2017"

- 在 64 位操作系统上，Key = HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSCommon\15.0\SQM 
- 在 32 位操作系统上，Key = HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSCommon\15.0\SQM 
- 启用“组策略”时，Key = HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM 

::: moniker-end

::: moniker range=">=vs-2019"

- 在 64 位操作系统上，Key = HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSCommon\16.0\SQM 
- 在 32 位操作系统上，Key = HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSCommon\16.0\SQM 
- 启用“组策略”时，Key = HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM 

::: moniker-end

Entry = OptIn 

Value = (DWORD)

- “0”为选择退出（关闭 VSCEIP） 
- “1”为选择加入（开启 VSCEIP） 

> [!CAUTION]
> 错误地编辑注册表可能会严重损坏您的系统。 更改注册表之前，应当备份计算机中的所有重要数据。 如果在应用手动更改之后遇到问题，也可以使用“最近一次的正确配置”启动选项  。

有关 VSCEIP 收集、处理或传输的信息的详情，请参阅 [Microsoft 隐私声明](https://privacy.microsoft.com/privacystatement)。

## <a name="see-also"></a>另请参阅

* [Visual Studio 收集的诊断信息](diagnostic-data-collection.md)
* [Visual Studio 反馈选项](../ide/feedback-options.md)
* [如何报告 Visual Studio 的问题](../ide/how-to-report-a-problem-with-visual-studio.md)
* [Visual Studio 开发者社区](https://developercommunity.visualstudio.com/)
* [Microsoft 隐私声明](https://privacy.microsoft.com/privacystatement)
