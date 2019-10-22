---
title: 将单元测试作为 64 位进程运行 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- unit tests, creating
- unit tests, running
ms.assetid: d23a9ee7-58e3-4e8b-a38c-b2207ea73fea
caps.latest.revision: 27
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fc379f522d119e76ef8be8ba60a4cc1482e57fd1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660467"
---
# <a name="run-a-unit-test-as-a-64-bit-process"></a>将单元测试作为 64 位进程运行
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你有一台 64 位计算机，则可以作为 64 位进程来运行单元测试并捕获代码覆盖率信息。

## <a name="running-a-unit-test-as-a-64-bit-process"></a>将单元测试作为 64 位进程运行

#### <a name="to-run-a-unit-test-as-a-64-bit-process"></a>将单元测试作为 64 位进程运行的具体步骤

1. 如果代码或测试是以 32 位/x86 形式编译，但现在希望将它们作为 64 位进程运行，请将它们重新编译为“任何 CPU”或“64 位”。

    > [!TIP]
    > 为了最大限度地提高灵活性，应使用“任何 CPU”配置来编译测试项目。 然后，可以在 32 位和 64 位代理上运行。 使用“64 位”配置编译测试项目毫无优势可言。

2. 在 Visual Studio 菜单中，依次选择“测试”、“设置”和“处理器体系结构”。 选择“x64”，将测试作为 64 位进程运行。

     \- 或 -

     在 .runsettings 文件中指定 `<TargetPlatform>x64</TargetPlatform>`。 此方法的一个优点是可以在不同文件中指定设置组，并在不同设置之间快速切换。 您还可以在解决方案之间复制设置。 有关详细信息，请参阅[使用 .runsettings 文件配置单元测试](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)。

## <a name="see-also"></a>请参阅
 [用测试资源管理单元运行单元测试](../test/run-unit-tests-with-test-explorer.md)[测试代码](../test/unit-test-your-code.md)[指定 Visual Studio 测试的测试设置](https://msdn.microsoft.com/library/0c15317e-80c6-4317-aed3-82b8e15e3901)
