---
title: 问题报表专用数据
ms.date: 06/21/2018
ms.topic: conceptual
helpviewer_keywords:
- developer community privacy
- privacy, developer community
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1e87f35778b8aec615410312c0eb7373d4e9969f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75775891"
---
# <a name="developer-community-data-privacy"></a>开发人员社区数据隐私

默认情况下，[开发者社区](https://developercommunity.visualstudio.com/)公开显示问题报告的所有信息，包括所有评论和回复。 这非常有用，因为这让整个社区都能看到其他用户发现的问题、绕过方法和解决方案。 但是，如果担心数据或身份隐私，可选择其他方式。

## <a name="identity-privacy"></a>身份隐私

如果担心身份泄露，请[新建一个 Microsoft 帐户](https://signup.live.com/)，该帐户不透露有关你的任何详细信息。 使用此帐户来创建报表。

## <a name="data-privacy"></a>数据隐私

如果担心数据隐私，请不要在初始报表的标题或内容中添加任何想要保密的内容，因为报告始终公开可见。 相反，请创建报表，并记得通过单独的评论以私密方式发送详细信息。 创建问题报表后，可指定谁可查看回复和附件：

1. 在创建的报表中，选择“添加评论”，创建对问题的私人说明  。

2. 在回复编辑器中，使用“提交”和“取消”按钮下的控件，指定可查看回复的群体   。 选择“版主和贴主可见”，可仅允许 Microsoft 员工和自己查看  。

   ![开发者社区上的“隐私”控件](media/developer-community-privacy-control.png)

   只有指定的人员能看到该评论及其内附的图像、链接或代码。 该评论下的所有回复与最初的评论具有相同的可见性。 即使回复上的隐私控件未正确显示可见性受限状态，仍是如此。

3. 添加重现所需的说明和所有其他信息、图像和文件附件。 选择“提交”按钮将私下发送此信息  。

   > [!NOTE]
   > 附件大小不得超过 2 GB，最多可附加 10 个文件。 如果需要上传更大的文件，可提交新的问题报表或在私人评论中上传 Microsoft 员工的 URL。

为了维护你的隐私，不暴露敏感信息，请可与 Microsoft 进行任何交互时，在可见性受限的评论下回复。 回复其他评论可能会导致敏感信息意外泄露。

## <a name="data-we-collect"></a>收集的数据

如果“报告问题”是由 Visual Studio 安装程序发出的，我们将收集最近的安装程序日志  。

如果“报告问题”是由 Visual Studio 安装程序发出的，我们将收集以下一种或多种类型数据  ：

- 事件日志中的 Watson 和 .NET 项

- Visual Studio 内存中活动日志文件

- PerfWatson 文件（如果启用 Watson 集合）

- LiveShare 日志文件（如果存在）

- Xamarin 日志文件（如果存在）

- Nuget 日志文件（如果存在）

- Web 调试程序日志文件（如果存在）

- 服务中心日志和 MEF 错误日志（如果存在）

- Python 日志（如果存在）

- Windows 窗体日志（如果存在）

- 屏幕截图（如果选择随附该项）

- 记录数据（如果选择包含记录），其中包括：

  - 问题重现步骤

  - ETL 跟踪文件

  - 转储文件

> [!NOTE]
> 你发送的日志文件、屏幕截图和记录数据可显著提高 Microsoft 对你的问题的理解和响应能力。  因此，建议将它们包含在内。 为保护你的隐私，仅当你提供权限（即提交包含任何附加的日志文件、屏幕截图和记录数据的问题报告）时，才会将这些日志文件、屏幕截图和记录数据发送给 Microsoft。 你可以在“报告问题”窗口的“摘要”步骤中查看哪些文件包含在内，然后再提交该报告。 你可以在“摘要”步骤中取消选中“附加系统日志”，从报告中排除系统日志文件。 有关参考信息，请参阅下面的屏幕截图。 
  > ![报告问题 - 收集的日志摘要](media/report-a-problem-logs-collected.png)


## <a name="see-also"></a>另请参阅

- [如何报告 Visual Studio 的问题](how-to-report-a-problem-with-visual-studio.md)
- [C++ 问题报表数据隐私](/cpp/how-to-report-a-problem-with-the-visual-cpp-toolset#reports-and-privacy)
