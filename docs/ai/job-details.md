---
title: 查看最近的作业
description: 了解提交作业后，可以查看作业列表，并查看作业状态和持续时间等。
ms.custom: SEO-VS-2020
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: d67ee5810c1776176e1370839f0f7f43b9d0c55e
ms.sourcegitcommit: 9c57730000d5ced37d3887f3928b17076f49d0f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2020
ms.locfileid: "92099214"
---
# <a name="view-recent-job-performance-and-details"></a>查看最近的作业性能和详细信息

提交作业后，可以查看作业列表，以查看作业状态和持续时间等。

1. 在“服务器资源管理器”中，展开特定计算上下文  。
2. 双击“作业”  。
3. 可看见提交到该计算上下文的作业列表。
4. 在列表中选择一个特定的作业以查看详细信息  。

![监视作业](media/job-details/monitor-jobs.png)

> 提交到 Linux VM 的作业历史记录存储在 VM 上的 /tmp 目录中。 因此，每次重启时都会清除作业历史记录。 要永久记录作业历史记录，请将 VM 配置为 Azure 机器学习中的计算上下文，然后将作业提交到 Azure 机器学习（选择 VM 作为计算上下文）。
