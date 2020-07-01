---
title: 克隆存储库
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: 9bb3aa4a7aa9818f42f99860956e0e2ae73b2b7f
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371581"
---
# <a name="clone-a-repository-of-python-code-in-visual-studio"></a>在 Visual Studio 中克隆 Python 代码存储库

安装 [Visual Studio Tools for AI](installation.md) 后，就可以轻松地克隆 Python 代码存储库并从中创建项目。

1. 要连接到 GitHub 存储库，请运行 Visual Studio 安装程序，选择“修改”，然后选择“单个组件”选项卡   。向下滚动到“代码工具”部分，选择“适用于 Visual Studio 的 GitHub 扩展”，然后选择“修改”    。

    ![在 Visual Studio 安装程序中选择 GitHub 扩展](media/create-project-repo/installation-github-extension.png)

2. 启动 Visual Studio。

3. 选择“视图”>“团队资源管理器”，打开“团队资源管理器”窗口，在该窗口中可以连接到 GitHub 或 Azure DevOps Services，或者克隆存储库   。

    ![显示 Azure DevOps、GitHub 并克隆存储库的“团队资源管理器”窗口](media/create-project-repo/team-explorer-devops.png)

4. 在“本地 Git 存储库”下的 URL 字段中，输入 `https://github.com/Microsoft/samples-for-ai`，为克隆文件输入一个文件夹，然后选择“克隆”   。

    > [!Tip]
    > 在团队资源管理器中指定的文件夹是用于接收克隆文件的特定文件夹。 与 `git clone` 命令不同，在团队资源管理器中创建克隆时不会使用存储库名称自动创建一个子文件夹。

5. 完成克隆后，双击团队资源管理器底部的存储库文件夹，导航到存储库仪表板。 在“解决方案”下方，选择“新建”   。

    ![“团队资源管理器”窗口，从克隆创建新项目](media/create-project-repo/team-explorer-new-project.png)

6. 在随即出现的“新建项目”对话框中，选择“从现有的 Python 代码”，为项目指定名称，将“位置”设置为与存储库相同的文件夹，并选择“确定”     。 在随即出现的向导中选择“完成”  。

7. 从菜单中选择“视图”>“解决方案资源管理器”  。

8. 在解决方案资源管理器中，展开 `TensorFlow Examples> MNIST` 节点，右键单击 `convolutional.py`，然后选择“设置为启动文件”  。 此步骤指示 Visual Studio 在运行项目时应使用哪个文件。

9. 按 Ctrl  +F5  ，或依次选择“调试”>“启动但不调试”  ，以运行程序。 如果发现错误，请在上一步中重新检查工作目录设置。

10. 程序成功运行时，可看见它开始下载培训和测试数据集，然后训练模型并输出错误率。 需要错误率随着时间推移降低

    ![Python MNIST 程序的第一次输出](media/create-project-repo/tensorflow-mnist-running.png)

   > [!NOTE]
   > 如果使用的是 Anaconda，并遇到指明缺少 numpy 的错误，可能需要[将 Python 环境更改为使用 Anaconda](../python/selecting-a-python-environment-for-a-project.md)。

11. 可以使用 TensorBoard 可视化进程。 右键单击项目，单击“运行 TensorBoard”，然后选择输出 TensorBoard 日志所在的目录  。

   ![运行 tensorboard](media/create-project-repo/run-tensorboard.png)

12. 请注意，错误随着时间推移而减少，这意味着质量在不断提高。

   ![运行 tensorboard](media/create-project-repo/tensorboard.png)
