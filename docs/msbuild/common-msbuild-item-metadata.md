---
title: 通用 MSBuild 项元数据 | Microsoft Docs
description: 了解对某些 MSBuild SDK 或目标具有意义的可选项元数据，默认情况下未针对每个项进行设置。
ms.custom: SEO-VS-2020
ms.date: 07/13/2020
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- msbuild, common item metadata
- item metadata (MSBuild)
ms.assetid: 9857505d-ae15-42f1-936d-6cd7fb9dd276
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 152967fb99442b58d96016e10d8899b57ef35bf6
ms.sourcegitcommit: bd9417123c6ef67aa2215307ba5eeec511e43e02
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92796585"
---
# <a name="common-msbuild-item-metadata"></a>通用 MSBuild 项元数据

下表介绍对某些 MSBuild SDK 或目标具有意义的可选项元数据，默认情况下未针对每个项进行设置。 可以设置这些项元数据以影响生成行为，但前提是你使用的 SDK 或目标文件可识别它。

| 项元数据 | SDK | 描述 |
|---------------| ------- | -------------|
|%(Link)| 全部 |Visual Studio 项目系统使用 `Link` 元数据（如果存在）来更改项目树中显示的内容；你可以在解决方案资源管理器中将文件放在不同的逻辑文件夹结构中。<br />此外，`AssignTargetPath` 任务将查看 `Link`，以确定在输出目录中将文件复制到的位置（如果它是复制的项之一）。|
|%(LinkBase)| .NET Core SDK | 用于设置要用于项组 `Link` 元数据的文件夹。 |

## <a name="see-also"></a>请参阅

- [常用的 MSBuild 项目属性](../msbuild/common-msbuild-project-properties.md)
- [常用的 MSBuild 项目项](../msbuild/common-msbuild-project-items.md)
- [MSBuild 常见的项元数据](msbuild-well-known-item-metadata.md)