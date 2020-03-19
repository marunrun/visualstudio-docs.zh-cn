---
title: 提交作业以在 Azure Batch AI 中训练模型
description: 训练模型云
keywords: ai, visual studio, 训练模型, 云
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 11/13/2017
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: dec70c9e9aeb9c916b511241a74b550354aff175
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75915776"
---
# <a name="train-ai-models-in-azure-batch-ai"></a>在 Azure Batch AI 中训练 AI 模型

Batch AI 是一种托管服务，使数据科学家和 AI 研究人员可以在 Azure 虚拟机（包括具有 GPU 支持的 VM）群集上训练 AI 和其他机器学习模型。 你只需描述作业的要求、用于查找输入和存储输出的位置，Batch AI 会处理其余部分。 [了解有关 Azure Batch AI 的详细信息](/azure/batch-ai/overview)

它与 Visual Studio Tools for AI 集成，以便你可以在 Azure 中动态横向扩展训练模型。  [安装 Visual Studio Tools for AI](installation.md) 之后，可以使用 Azure 机器学习示例库中的预制方案轻松地创建新 Python 项目。

1. 启动 Visual Studio。 通过打开“AI 工具”菜单，然后选择“选择群集”，来打开“服务器资源管理器”   

    ![群集选择器](media/train-model/select-cluster.png)

2. 展开“AI 工具”  。 你具有的任何 Batch AI 资源都会自动检测到并出现在服务器资源管理器中。

    ![示例库](media/train-model/batchai.png)

3. 选择“视图”>“团队资源管理器...”，打开“团队资源管理器”窗口，可在该窗口中连接到 GitHub 或 Azure DevOps Services，或者克隆存储库   。

    ![显示 Azure DevOps、GitHub 并克隆存储库的“团队资源管理器”窗口](media/train-model/team-explorer-devops.png)

4. 在“本地 Git 存储库”下的 URL 字段中，输入 `https://github.com/Microsoft/samples-for-ai`，为克隆文件输入一个文件夹，然后选择“克隆”   。

    > [!Tip]
    > 在团队资源管理器中指定的文件夹是用于接收克隆文件的特定文件夹。 与 `git clone` 命令不同，在团队资源管理器中创建克隆时不会使用存储库名称自动创建一个子文件夹。

5. 克隆完成后，单击“文件”>“打开解决方案”>“项目/解决方案” 

    ![示例库](media/train-model/open-solution.png)

6. 打开克隆存储库的目录中的 samples-for-ai\TensorFlowExamples\TensorFlowExamples.sln 

    ![示例库](media/train-model/tensorflowexamples.png)

7. 将 MNIST 项目设置为“启动项目” 

    ![示例库](media/train-model/mnist-startup.png)

8. 右键单击“MNIST 项目”的“提交作业”   

    ![示例库](media/train-model/submit-job.png)
9. 选择“Azure Batch AI”  群集，然后单击“导入”  。 选择 `AzureBatchAI_TF_MNIST.json` 文件以快速填充一些默认值，如要使用的 Docker 映像。 然后单击“提交” 

    ![示例库](media/train-model/submit-batch.png)
