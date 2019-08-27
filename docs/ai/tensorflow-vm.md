---
title: 在云中运行 TensorFlow 模型
description: 在 Azure 深入学习 VM 中运行 tensorflow 模型
keywords: ai, visual studio, 深入学习虚拟机
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 11/13/2017
ms.topic: tutorial
ms.devlang: python
ms.workload:
- multiple
ms.openlocfilehash: adb3720f1624f355b99d75bfe446fafab1c5e0ae
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62427527"
---
# <a name="train-a-tensorflow-model-in-the-cloud"></a>在云中训练 TensorFlow 模型

在本教程中，我们会在 Azure [深入学习](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview)虚拟机上使用 [MNIST 数据集](http://yann.lecun.com/exdb/mnist/)训练 TensorFlow 模型。

MNIST 数据库具有包含 60,000 个示例的训练集，以及包含 10,000 个手写数字示例的测试集。

## <a name="prerequisites"></a>系统必备
开始之前，确保安装和配置了以下各项：

### <a name="setup-azure-deep-learning-virtual-machine"></a>设置 Azure 深入学习虚拟机

> [!NOTE]
> 将“操作系统类型”设置为 Linux。

可以在[此处](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/provision-deep-learning-dsvm)找到用于设置深入学习虚拟机的说明。

### <a name="remove-comment-in-parens"></a>删除括号中的注释

```bash
echo -e ". /etc/profile\n$(cat ~/.bashrc)" > ~/.bashrc
```

### <a name="download-sample-code"></a>下载示例代码

首先下载此 [GitHub 存储库](https://github.com/Microsoft/samples-for-ai)，在其内附的示例中深入了解 TensorFlow、CNTK、Theano 等工具。

## <a name="open-project"></a>打开项目

- 启动 Visual Studio，选择“文件”>“打开”>“项目/解决方案”。

- 在下载的示例存储库中选择 Tensorflow Examples 文件夹，然后打开 TensorflowExamples.sln 文件。

   ![打开项目](media/tensorflow-local/open-project.png)

   ![打开解决方案](media/tensorflow-local/open-solution.png)

## <a name="add-azure-remote-vm"></a>添加 Azure 远程 VM

在服务器资源管理器中，右键单击“AI 工具”下的“远程计算机”节点，然后选择“添加...”。 输入远程计算机显示名称、IP 主机、SSH 端口、用户名和密码/密钥文件。

![添加新远程计算机](media/tensorflow-vm/add-remote-vm.png)

## <a name="submit-job-to-azure-vm"></a>将作业提交到 Azure VM
在“解决方案资源管理器”中右键单击 MNIST 项目，然后选择“提交作业”。

![将作业提交到远程计算机](media/tensorflow-vm/job-submission.png)

在提交窗口中：

- 在“要使用的群集”列表中，选择要将作业提交到的远程计算机（具有“rm:”前缀）。

- 输入“作业名称”。

- 单击“提交”。

## <a name="check-status-of-job"></a>检查作业的状态
查看作业的状态和详细信息：在“服务器资源管理器”中展开将作业提交到的虚拟机。 双击“作业”。

![作业浏览器](media/tensorflow-vm/job-browser.png)

## <a name="clean-up-resources"></a>清理资源

如果你计划在不久的将来进行使用，则停止 VM。 如果要完成本教程，则运行以下命令以清理资源：

```azurecli-interactive
az group delete --name myResourceGroup
```
