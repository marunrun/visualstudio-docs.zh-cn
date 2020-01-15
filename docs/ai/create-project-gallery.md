---
title: 创建项目
description: 使用 Azure 机器学习库中的示例创建项目
keywords: ai, visual studio, azure 机器学习
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 11/13/2017
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: d5e73757e10eec5e7e8c290772822f49129fd1e5
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75915904"
---
# <a name="create-an-ai-project-from-the-azure-machine-learning-gallery-in-visual-studio"></a>在 Visual Studio 中通过 Azure 机器学习库创建 AI 项目

Azure 机器学习与 Visual Studio Tools for AI 集成在一起。 可以使用它将机器学习作业提交到远程计算目标，如 Azure 虚拟机、Spark 群集等。 

[安装 Visual Studio Tools for AI](installation.md) 之后，可以使用 Azure 机器学习示例库中的预制方案轻松地创建新 Python 项目。

> [!NOTE]
> 必须安装 Azure 机器学习工作台。 要进行安装，请参阅 [Azure 机器学习安装快速入门](/azure/machine-learning/preview/quickstart-installation)

1. 启动 Visual Studio。 通过打开“AI 工具”菜单，然后选择“选择群集”，来打开“服务器资源管理器”   

    ![群集选择器](media/create-project-gallery/select-cluster.png)

2. 通过在服务器资源管理器中右键单击“Azure 机器学习”节点，然后选择“登录”并按照说明进行操作，来登录 Azure 机器学习订阅   。

    ![登录](media/create-project-gallery/azureml-login.png)

3. 选择“AI 工具”>“Azure 机器学习示例库”  。

    ![示例库](media/create-project-gallery/gallery.png)

4. 对于本快速入门，选择“使用 TensorFlow 的 MNIST”示例，然后单击“安装”   。 提供以下内容：

   - **资源组**：存储元数据的 Azure 资源组
   - **帐户**：Azure 机器学习试验帐户
   - **工作区**：Azure 机器学习工作区
   - **项目类型**：机器学习框架。 在此例中选择“TensorFlow” 
   - **添加到解决方案**：确定是添加到当前 Visual Studio 解决方案还是创建并打开新解决方案
   - **项目路径**：保存代码的位置
   - **项目名称**：键入 TensorFlowMNIST 

   ![使用 Python 应用程序模板时生成的项目](media/create-project-gallery/new-AzureSampleProject.png)

5. Visual Studio 随即创建项目文件（磁盘上的 `.pyproj` 文件）以及示例中定义的其他文件。 对于“MNIST”模板，项目包含多个文件。

    ![mnist](media/create-project-gallery/azml-mnist.png)

6. 将作业提交到 Azure 机器学习。

    ![mnist](media/create-project-gallery/submit-azml.png)

7. 在 Docker 容器中或本地计算机上运行

    ![mnist](media/create-project-gallery/azml-local.png)
