---
title: 浏览存储以上传数据
description: 了解如何在远程计算机或 Azure 文件共享上访问所有存储，以上传数据或下载模型和日志。
ms.custom: SEO-VS-2020
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: ae419c67b493ef03b08f6fcf627ad0fbe42ca6d0
ms.sourcegitcommit: 9c57730000d5ced37d3887f3928b17076f49d0f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2020
ms.locfileid: "92099201"
---
# <a name="browse-storage-to-upload-data-or-download-models-and-logs"></a>浏览存储以上传数据或下载模型和日志

可以在远程计算机或 Azure 文件共享上访问所有存储，以上传数据或下载模型和日志。 或者，如果要访问特定作业的日志和作业输出，也可以在作业浏览器中执行相同的操作。

## <a name="to-access-all-data-on-the-remote-machine-or-file-share"></a>访问远程计算器或文件共享上的所有数据

1. 打开“服务器资源管理器”。
2. 展开远程计算机或 Batch AI 计算上下文。
3. 右键单击“存储”；然后单击“浏览” 。

    ![storage](media/manage-storage/browse-storage.png)

## <a name="to-access-job-specific-data-on-the-remote-machine-or-file-share"></a>在远程计算机或文件共享上访问作业特定数据

1. 打开 [“作业历史记录”](job-details.md)
2. 选择作业。
3. 单击“工作文件夹”，或单击 StdOut/Stderr 快速访问这些重要的日志文件 。

    ![storage](media/manage-storage/job-workingfolder.png)
