---
title: 如何报告 Visual Studio 的问题
description: 了解如何报告 Visual Studio 的问题
ms.date: 03/11/2018
ms.topic: how-to
ms.assetid: bee01179-cde5-4419-9095-190ee0ba5902
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2e5f64ebdf93384b7def728ac5d01bcbaf6b0271
ms.sourcegitcommit: 98af63c1a53a732558f8207338dc2722abbbe49e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88584533"
---
# <a name="how-to-report-a-problem-with-visual-studio-or-visual-studio-installer"></a>如何报告 Visual Studio 或 Visual Studio 安装程序的问题

> [!NOTE]
> 对于 Visual Studio for Mac，请参阅[如何报告 Visual Studio for Mac 的问题](/visualstudio/mac/report-a-problem)。

可以通过 Visual Studio 或其安装程序报告问题。 利用内置的反馈工具，你可以轻松添加可帮助 Visual Studio 团队诊断和修复问题的诊断信息。 下面是报告问题的步骤。

1. 在 Visual Studio 中，选择右上角的反馈图标并选择“报告问题”。 此外可以从菜单“帮助” > “发送反馈” > “报告问题”来访问反馈工具。
![Visual Studio 开发人员社区中的“报告问题”弹出窗口](media/feedback-button.png) 或者，如果无法安装 Visual Studio 或无法访问 Visual Studio 中的反馈工具，则在 Visual Studio 安装程序中报告问题。  在安装程序中，选择右上角的反馈图标并选择“报告问题”。
![Visual Studio 开发人员社区中的“报告问题”弹出窗口](media/installer.png)

1. 单击“报告问题”将打开默认浏览器，并使用登录 Visual Studio 时使用的同一帐户登录

   ![登录以报告问题](../ide/media/feedback-browser-top.png)

1. 首先输入 bug 报告的描述性标题。 它的长度必须至少为 25 个字符。

    ![报告问题](../ide/media/feedback-report.png)

1. 开始键入后，“标题”字段下会显示可能的重复项

    ![搜索重复项](../ide/media/feedback-search.png)

1. 选择可能的重复 bug 报告，查看是否存在与自己的问题匹配的项。 如果存在，则为其投票，而非创建自己的票证。

    ![为重复项投票](../ide/media/feedback-duplicate.png)

2. 如果未找到任何重复项，则继续输入问题的说明。 尽可能清楚地说明问题，使我们更有可能重现 bug，这一点很重要。 请确保包含清晰的重现步骤。

3. 如果与 bug 报告相关，请通过选中“包括 Visual Studio 屏幕截图”复选框来抓取屏幕截图。

    ![抓取屏幕截图](../ide/media/feedback-screenshot.png)仅 Microsoft 工程师可以查看此屏幕截图

    你甚至可以直接在浏览器中裁剪屏幕截图，以删除任何敏感或无关的部分。

4. 要帮助 Visual Studio 工程团队解决问题，最佳方法之一是提供跟踪和堆转储文件供其查看。 可以通过记录导致 bug 的步骤轻松执行此操作。 

    ![记录你的操作](../ide/media/feedback-recording.png)仅 Microsoft 工程师可以查看该记录

5. 查看附加的文件，并上传其他文件（如果你认为这有助于诊断问题）。   

    ![附加的文件](../ide/media/feedback-attachments.png)仅 Microsoft 工程师可以查看附加的文件

6. 最后一步是点击“提交”按钮。 提交报告会直接将报告发送到内部 Visual Studio bug 报告系统等待会审。

## <a name="when-further-information-is-needed"></a>如果需要进一步信息

如果问题缺少重要信息，我们将分配“需要更多信息”状态。 我们将在问题上评论称我们需要该特定信息，你也将收到电子邮件通知。 如果我们在 7 天内未收到该信息，将向你发送提醒。 之后，如果你 14 天内未操作，我们将关闭该票证。

1. 访问电子邮件中指向问题报告的链接，或者转到“我的反馈”，以查看处于“需要详细信息”状态的所有报告。

    ![我的反馈](../ide/media/feedback-my-feedback.png)

1. 选择问题报告上的“提供详细信息”链接将导航到新屏幕。 在该屏幕中，可以看到请求的信息。

   ![我的反馈](../ide/media/feedback-need-more-info.png)

1. 可以通过添加注释、附件或记录步骤来提供更多信息。 此体验类似于报告新问题或在对问题进行投票时提供其他信息。

1. 提供额外信息后，发出请求的 Microsoft 工程师会收到相关通知。 如果获取的信息足以开展调查，问题状态随即更改。 否则，工程师会要求提供更多信息。

在“我的反馈”屏幕上可以查看这些请求，以及其他所有“问题”和“建议”  。

## <a name="search-for-solutions-or-provide-feedback"></a>搜索解决方案或提供反馈

如果不希望或不能使用 Visual Studio 报告问题，可能 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/)页上已报告此问题并且已发布解决方案。

如果没有要报告的问题但希望建议一项功能，也可以在此处提供反馈。 有关详细信息，请参阅[建议一项功能](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)页面。

## <a name="see-also"></a>请参阅

* [开发者社区指南](https://docs.microsoft.com/visualstudio/ide/developer-community-guidelines)
* [Visual Studio 反馈选项](../ide/feedback-options.md)
* [报告 Visual Studio for Mac 的问题](/visualstudio/mac/report-a-problem)
* [报告 C++ 问题](/cpp/how-to-report-a-problem-with-the-visual-cpp-toolset)
* [Visual Studio 开发者社区](https://developercommunity.visualstudio.com/)
* [开发人员社区数据隐私](developer-community-privacy.md)
