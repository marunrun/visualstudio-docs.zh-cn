---
title: MSBuild 中的日志记录 | Microsoft Docs
description: 了解 MSBuild 日志记录如何让你能够通过在日志文件中捕获生成事件、消息、警告和错误来监视生成进度。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- msbuild, logging
ms.assetid: 9aea2e76-8f60-4234-913d-598e7bbad808
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9de830003571f1f648cf06be634d9a773b95269f
ms.sourcegitcommit: f1d47655974a2f08e69704a9a0c46cb007e51589
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92904331"
---
# <a name="logging-in-msbuild"></a>MSBuild 中的日志记录

通过日志记录可监视生成的进度。 日志记录捕获日志文件中的生成事件、消息、警告和错误。

## <a name="in-this-section"></a>在本节中

- [获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)

 描述 MSBuild 中日志记录的各个方面。

- [生成记录器](../msbuild/build-loggers.md)

 概述创建单处理器记录器所需的步骤。

- [多处理器环境下的日志记录](../msbuild/logging-in-a-multi-processor-environment.md)

 介绍日志记录在多处理器环境和两个多处理器日志记录模型下的工作原理。

- [编写可识别多处理器的记录器](../msbuild/writing-multi-processor-aware-loggers.md)

 概述如何创建多处理器感知记录器以及如何使用可配置的转发记录器。

- [创建转发记录器](../msbuild/creating-forwarding-loggers.md)

 概述如何创建自定义转发记录器。

## <a name="see-also"></a>另请参阅

- [并行生成多个项目](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md) 介绍如何通过并行运行多个项目来更快地生成它们。
