---
title: 开发者社区指南
description: 介绍 VisualStudio 开发者社区的使用指南。
ms.date: 6/30/2020
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ed52bcbd6d27a958276541c2d6813aa322c73839
ms.sourcegitcommit: a466720759426265b18b0f8d74a970e72493d700
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86092292"
---
# <a name="developer-community-guidelines"></a>开发者社区指南

开发者社区负责跟踪 Visual Studio 的问题和功能建议。

## <a name="submitting-problems-and-suggestions"></a>提交问题和建议

[Visual Studio 开发者社区](https://developercommunity.visualstudio.com/)负责跟踪 Visual Studio 的问题和功能建议。

### <a name="before-submitting-an-issue"></a>提交问题前

在 Visual Studio 开发者社区中搜索你的问题，确保该问题尚不存在。 如果你发现你的问题已存在，请发表相关评论并进行投票。

如果没有你的问题，请使用 visual-studio 标记在 [Stack Overflow](https://stackoverflow.com/questions/tagged/visual-studio?tab=Newest) 上向社区提问。 我们有客户支持人员监视标记，他们将帮助回答问题。

如果发现当前没有问题来描述你遇到的 bug 或要建议的功能，请按照以下指南提问。

### <a name="writing-a-good-bug-report-or-feature-suggestion"></a>编写一个好的 bug 报告或功能建议

- 每项只提交一个问题或功能请求。

  - 将多个问题或功能请求合并为一项会增加我们诊断的难度，也让其他用户更难投票支持你的内容。
  - 不要将你的问题作为评论添加到现有问题中，除非它针对的是相同的输入信息。 许多问题看起来相似，但原因不同，因此上述操作将使得我们更难诊断你的问题。

- 你可提供的信息越多，我们就越容易重现和解决你的问题。
- 随附每个问题提供以下步骤。

  - 可重现步骤 (1...2...3...)，还有你预期的结果及你遇到的结果。
  - 图像、动画或视频链接。 图像和动画可演示重现步骤，但不取代它们。
  - （视情况而定）可演示问题的代码片段，或者我们可轻松拉取到我们的计算机上来重新创建问题的代码存储库的链接。

- 请记得执行以下步骤：

  - 搜索查看是否存在重复内容。 如果存在，请投票支持现有问题，根据需要提供其他评论或说明。
  - 重新创建在禁用扩展后出现的问题。 如果你发现问题是由安装的扩展引起的，请单独就该扩展提问。
  - 简化围绕问题的代码，让我们能更好地划分出该问题。

即使提供的问题细节很丰富，我们也可能没法重现问题，并可能要求提供更多信息！

## <a name="managing-problem-reports"></a>管理问题报告

会审问题这一过程涉及多个步骤，是在功能团队中协作完成的。 会审通常需要一周时间，但也可能要花更长时间。 会审的目标是让你明白我们将如何处理你的问题。 例如，在会审后，你知道我们是计划解决你的问题还是计划等待更多社区反馈。

报告问题后，可通过状态了解你的提交在其生命周期中所处的位置。 Visual Studio 产品团队在评审你的反馈时，会将它设为适当的状态。 可查看[问题状态和常见问题解答](https://docs.microsoft.com/visualstudio/ide/report-a-problem)来跟踪问题报告的进度。

如果问题缺少重要信息，我们将分配“需要更多信息”状态。 我们将在问题上评论称我们需要该特定信息，你也将收到电子邮件通知。 如果我们在 7 天内未收到该信息，将向你发送提醒。 之后，如果你 14 天内未操作，我们将关闭该票证。

### <a name="wont-fix-bugs"></a>不修复 bug

如果某些 bug 所耗的成本大于效益，我们将关闭它们。 例如，如果修复太复杂，可能导致很多用户的性能下降，则修复可能就不合理。 当我们关闭这类 bug 时，会解释原因。

### <a name="other-product"></a>其他产品

有时在报告问题时，发现它是由其他产品引起的，与 Visual Studio 无关。 可能是其他的相关应用程序或某个扩展。 

发生这种情况时，我们将关闭该问题，并要求你就其他产品提问。 下面是可提出这些问题的一些常见位置：

* [SQL Server](https://feedback.azure.com/forums/908035-sql-server)
* [Visual Studio 订阅支持](https://feedback.azure.com/forums/908035-sql-server)
* [Office](https://support.office.com/article/how-do-i-give-feedback-on-microsoft-office-2b102d44-b43f-4dd2-9ff4-23cf144cfb11)
* [窗口](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)

#### <a name="additional-information"></a>其他信息

- [如何提高性能问题被解决的几率](https://docs.microsoft.com/visualstudio/ide/how-to-increase-chances-of-performance-issue-being-fixed)
- [排查 MSBuild 问题并为其创建日志](https://docs.microsoft.com/visualstudio/ide/msbuild-logs)

## <a name="managing-feature-suggestions"></a>管理功能建议

功能建议是我们与开发者社区成员之间交流的一种方式。 从技术上讲，我们可永远将所有功能请求保持在打开状态。 但如果保持问题不关闭，社区成员会更难看到某项功能的实际状态。 因此，我们会关闭不处理的功能请求，向我们可能要处理的功能分配“正在评审”标签。

如果你建议了一项功能，而我们不打算处理你的请求，你可能会感到失望。 我们了解到这一点。 我们所有人都在这里，要不在这个项目中，要不在我们参与的其他项目中。 因此请放心，我们乐于收到你提供的任何建议。 如果关闭你的建议或对其分配“正在评审”标签，请不要生气。 如果你认为你的功能建议值得保留，请删除你的使用场景，并联系我们或收集更多支持票。

在我们的决策过程中，我们将查看关于功能建议的下列特征：

- 我们能负担得起构建和维护它的费用吗？
- 它符合我们的总体[路线图](https://docs.microsoft.com/visualstudio/productinfo/vs-roadmap)策略吗？
- 如投票和评论所示，它得到社区的支持了吗？
- 即使社区支持度低，我们还是喜欢它吗？

如果我们对其中任一问题没法给出“是”的答案，我们就会关闭它。 但建议通常保持在“正在评审”状态下打开，以收集更多社区反馈。

可查看[建议状态和常见问题解答](https://docs.microsoft.com/visualstudio/ide/report-a-problem)来跟踪功能建议的进度。

## <a name="discussion-etiquette"></a>讨论礼节

为保持对话清晰、透明，请只用英语讨论，讨论内容与问题相关。 请体谅他人，尽量礼貌、专业。

有关详细信息，请参阅 [Microsoft 社区行为准则](https://answers.microsoft.com/en-us/page/codeofconduct)。

任何违反讨论礼节的行为都可能导致删评并最终对相关用户禁言。

## <a name="data-privacy"></a>数据隐私

评论和回复公开可见，但任何附加的文件仅私下与 Microsoft 共享。 公开这些信息很有益，可让所有社区成员看到其他用户发现的问题和解决方案。 如果担心数据或身份隐私，可选择其他方式。 详细了解[开发者社区数据隐私](https://docs.microsoft.com/visualstudio/ide/developer-community-privacy)。

## <a name="next-steps"></a>后续步骤

前往 [Visual Studio 开发者社区](https://developercommunity.visualstudio.com/)报告问题、建议功能或浏览现有票证。 请尽情体验吧！
