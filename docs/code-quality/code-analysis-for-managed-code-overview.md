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
ms.openlocfilehash: e6515c0df7a9c3389e754d5238788d716be49e2e
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88800081"
---
# <a name="overview-of-code-analysis-for-managed-code-in-visual-studio"></a>Visual Studio 中托管代码的代码分析概述

Visual Studio 可通过两种方式对托管代码执行代码分析：
- 对于 [传统分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)，也称为 FxCop 静态分析托管程序集。
- 具有更现代的 [基于 .NET Compiler Platform 的代码分析器](../code-quality/roslyn-analyzers-overview.md)。 基于 .NET Compiler Platform 的代码分析器（在你键入时实时分析你的代码）将替换旧的 FxCop 静态代码分析，后者仅分析已编译的代码。