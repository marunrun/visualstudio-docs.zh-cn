---
title: 如何报告 Visual Studio 的问题
description: 了解如何报告 Visual Studio 的问题
ms.date: 03/11/2018
ms.topic: conceptual
ms.assetid: bee01179-cde5-4419-9095-190ee0ba5902
ms.author: seiyer
author: seaniyer
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 97080d4ee2240725f009505cda8429ba8f5975d5
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "64556719"
---
# <a name="how-to-report-a-problem-with-visual-studio-or-visual-studio-installer"></a>如何报告 Visual Studio 或 Visual Studio 安装程序的问题

> [!NOTE]
> 对于 Visual Studio for Mac，请参阅[如何报告 Visual Studio for Mac 的问题](/visualstudio/mac/report-a-problem)。

可以使用 Visual Studio 或其安装程序中包含的反馈工具报告问题。 反馈工具使你能够轻松地在反馈中包含诊断信息，并帮助 Visual Studio 团队更有效地诊断和修复问题。 下面是报告问题的步骤。

1. 在 Visual Studio 中  ，选择右上角的反馈图标并选择“报告问题”。 此外可以从菜单“帮助”   > “发送反馈”   > “报告问题”  来访问反馈工具。
![Visual Studio 开发人员社区中的“报告问题”弹出窗口](media/vsfeedbackentry.png) 或者，如果无法安装 Visual Studio 或无法访问 Visual Studio 中的反馈工具，则在 Visual Studio 安装程序  中报告问题。  在安装程序中，选择右上角的反馈图标并选择“报告问题”。
![Visual Studio 开发人员社区中的“报告问题”弹出窗口](media/installer.png)

1. 如果未登录，请选择“登录”  ，如以下屏幕截图所示。 按照屏幕上的说明登录。

   ![登录以报告问题](../ide/media/sign-in-new-ux.png)

   不仅可以在登录时报告问题，还可以对任何现有反馈进行投票和评论。

1. 登录后，可在“我关注的项”  屏幕上看到自己的“问题”  和“活动” 

   ![我关注的项](../ide/media/items-i-follow.png)

1. Visual Studio 提供了一个界面，用于搜索问题并查看其他人是否已报告该问题。 如果有人已报告此问题，请为其“投票”以便让我们知道。
   > [!NOTE]
   > 若要搜索，请在搜索框中输入所需文本，然后单击 Enter 或按“搜索”图标。

   ![搜索类似的问题并为其投票](../ide/media/search-and-vote.png)

1. 如果未找到所遇到的问题，请选择屏幕底部的“报告新问题”  。

   > [!NOTE]
   > “报告新问题”按钮仅出现在开发人员社区的 Visual Studio 界面中  。 无法直接在[开发人员社区](https://developercommunity.visualstudio.com/)网站上报告问题。

1. 为此问题创建一个描述性标题，帮助我们将其发送到正确的 Visual Studio 团队。

1. 向我们提供任何其他详细信息，如有可能，请同时提供再现该问题的步骤。

   ![报告新问题](../ide/media/report-new-problem.png)

1. 选择“下一步”，移至“附件”选项卡   。在此处，可截取当前屏幕并将其发送给 Microsoft。 若要附加其他屏幕截图或其他文件，请选择“附加其他文件”  。

   ![将屏幕截图附加到 Visual Studio 问题报告](media/report-a-problem-screenshot.png)

1. 如果不想附加屏幕截图或[记录重现](#record-a-repro)，请选择“下一步”移至“摘要”选项卡   。

1. 单击“提交”发送报告，以及任何图像和跟踪或转储文件  。 （如果“提交”按钮为灰色，请确保你已提供报告的标题和说明。  ）

   有关所收集数据的信息，请参阅[我们收集的数据](developer-community-privacy.md#data-we-collect)。

## <a name="record-a-repro"></a>记录重现

跟踪和堆转储文件在帮助我们诊断问题方面很有用。 如果你使用“报告问题”  工具记录重现步骤并将数据发送给 Microsoft，我们非常感激。 以下是操作方法：

1. 输入问题的标题和说明后，选择“下一步”移至“附件”选项卡   。

1. 选择“记录”选项卡  。

1. 在“记录操作”下，如果可在这里重现问题，请选择 Visual Studio 的当前实例  。 如果不能（例如 Visual Studio 挂起），请选择“\<创建新实例>”，在新的 Visual Studio 实例中记录操作  。

1. 选择“开始记录”  。 授予运行该工具的权限。

   ![选择“开始录制”，在 Visual Studio 问题报告中提供跟踪和堆转储文件](../ide/media/record-dialog-box.png)

1. 显示**步骤记录器**工具后，执行重现问题的步骤。

1. 完成后，选择“停止记录”按钮  。

1. 请等待几分钟时间，以便 Visual Studio 收集和打包已记录的信息。

   有关所收集数据的信息，请参阅[我们收集的数据](developer-community-privacy.md#data-we-collect)。

## <a name="when-further-information-is-needed-need-more-info"></a>如果需要进一步信息（需要更多信息）

从 Visual Studio 2017 版本 15.5 开始，提供了新的工作流以帮助用户提供有关问题报告的其他信息。

1. Microsoft 工程师将 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/)问题设置为“需要更多信息”状态后，发布、投票、关注或评论该问题的任何用户都会在 Visual Studio 中的“报告问题”工具中收到通知   。

   ![Visual Studio 中的“需要更多信息”通知](../ide/media/nmi-notification.png)

1. 单击“查看问题链接”可对问题进行筛选和排序，值查看需要注意的问题  。 问题旁边还有一个指示符，可在常规搜索中以此区分问题。

1. 单击问题可查看问题详细信息视图。

   ![“需要更多信息”通知](../ide/media/nmi-details-view.png)

1. 若要查看“需要更多信息”请求，请单击问题详细信息视图中的“查看他们的请求和回复”链接   。 对话框将显示请求。

   ![“需要更多信息”通知](../ide/media/nmi-request.png)

1. 可以通过添加注释、附件或记录步骤来提供更多信息。 此体验类似于报告新问题或在对问题进行投票时提供其他信息。

1. 提供额外信息后，发出请求的 Microsoft 工程师会收到相关通知。 如果获取的信息足以开展调查，问题状态随即更改。 否则，工程师会要求提供更多信息。

   > [!NOTE]
   > * 进行回复时，通知将会消失。 取而代之的是一条横幅，其中表达了感谢并介绍了提供更多信息的方法。
   > * 问题状态更改后，所有关注此问题的人收到的该通知都会消失。
   > * 可以多人回复同一“需要更多信息”请求  。
   > * 如果通过 Web 浏览器直接访问[开发人员社区](https://developercommunity.visualstudio.com/)，那么其上没有“需要更多信息”工作流，但也可以提供评论和附件  。

## <a name="search-for-solutions-or-provide-feedback"></a>搜索解决方案或提供反馈

如果不希望或不能使用 Visual Studio 报告问题，可能 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/)页上已报告此问题并且已发布解决方案。

如果没有要报告的问题但希望建议一项功能，也可以在此处提供反馈。 有关详细信息，请参阅[建议一项功能](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)页面。

## <a name="see-also"></a>请参阅

* [Visual Studio 反馈选项](../ide/feedback-options.md)
* [报告 Visual Studio for Mac 的问题](/visualstudio/mac/report-a-problem)
* [报告 C++ 问题](/cpp/how-to-report-a-problem-with-the-visual-cpp-toolset)
* [Visual Studio 开发者社区](https://developercommunity.visualstudio.com/)
* [开发人员社区数据隐私](developer-community-privacy.md)
