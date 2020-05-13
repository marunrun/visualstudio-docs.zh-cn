---
title: 单元测试 Python 代码
description: 在 Visual Studio 中为 Python 代码设置单元测试，以充分利用测试资源管理器功能来发现、运行和调试测试。
ms.date: 09/18/2019
ms.topic: include
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 09c67ace9db36cb8ee3d94296d339b62849e3c94
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "71254201"
---
# <a name="set-up-unit-testing-for-python-code"></a>为 Python 代码设置单元测试

单元测试是测试应用程序中其他代码单元的代码片段，通常为独立函数、类等。 应用程序通过其所有单元测试后，至少可以相信其低级功能正确无误。

Python 单元测试广泛应用于在程序设计期间验证方案。 针对 Visual Studio 的 Python 支持包括在开发过程的上下文中发现、执行和调试单元测试，无需单独运行单元测试。

本文简要介绍了适用于 Python 语言的 Visual Studio 中的单元测试功能。 有关单元测试的的更多常见信息，请参阅[对代码进行单元测试](../test/unit-test-your-code.md)。

::: moniker range="vs-2017"

[!include[Testing Python code](includes/vs-2017/unit-testing-python.md)]

::: moniker-end

::: moniker range=">= vs-2019"

[!include[Testing Python code](includes/vs-2019/unit-testing-python.md)]

::: moniker-end