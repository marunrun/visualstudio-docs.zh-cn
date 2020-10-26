---
title: 使用 TensorBoard 监视
description: 了解如何使用 Visual Studio 通过 TensorBoard 直观显示模型培训进度。
ms.custom: SEO-VS-2020
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: a9242cdd4a09b7d0cb1cae1904800696dc9c3d82
ms.sourcegitcommit: 9c57730000d5ced37d3887f3928b17076f49d0f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2020
ms.locfileid: "92099175"
---
# <a name="monitor-with-tensorboard"></a>使用 TensorBoard 监视

可以使用 TensorBoard 可视化模型培训进度。

1. 右键单击项目，单击“运行 TensorBoard”；然后选择输出 TensorBoard 日志所在的目录  。

    ![运行 tensorboard](media/monitor-tensorboard/run-tensorboard.png)

2. 可注意到，错误随着时间推移减少，这意味着质量在不断提高。

    ![运行 tensorboard](media/monitor-tensorboard/tensorboard.png)
