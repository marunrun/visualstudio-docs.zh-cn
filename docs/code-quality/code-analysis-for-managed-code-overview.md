---
title: 托管代码分析
ms.date: 06/12/2019
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: f4e5aad0ffcd6febce411d952b1b36a0669b109a
ms.sourcegitcommit: bb72ce6ec173f3ae06c7ae57322c43690f27553c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2020
ms.locfileid: "76967311"
---
# <a name="overview-of-code-analysis-for-managed-code-in-visual-studio"></a>Visual Studio 中托管代码的代码分析概述

Visual Studio 可以通过以下两种方式对托管代码执行代码分析：通过[传统分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)（也称为 FxCop 静态分析）托管程序集，以及更新式的[基于 .NET Compiler Platform 的代码分析器](../code-quality/roslyn-analyzers-overview.md)。 基于 .NET Compiler Platform 的代码分析器（在你键入时实时分析你的代码）将替换旧的 FxCop 静态代码分析，后者仅分析已编译的代码。

