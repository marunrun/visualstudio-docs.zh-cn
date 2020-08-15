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
ms.openlocfilehash: 901c66a97a763345ee32b1a1540a7998934d0ff3
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88248975"
---
# <a name="overview-of-code-analysis-for-managed-code-in-visual-studio"></a>Visual Studio 中托管代码的代码分析概述

Visual Studio 可以通过以下两种方式对托管代码执行代码分析：通过 [传统分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)（也称为 FxCop 静态分析）托管程序集，以及更新式的 [基于 .NET Compiler Platform 的代码分析器](../code-quality/roslyn-analyzers-overview.md)。 基于 .NET Compiler Platform 的代码分析器（在你键入时实时分析你的代码）将替换旧的 FxCop 静态代码分析，后者仅分析已编译的代码。
