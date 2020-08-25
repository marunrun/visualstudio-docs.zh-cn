---
title: 将单元测试作为 64 位进程运行
ms.date: 03/10/2020
ms.topic: how-to
helpviewer_keywords:
- unit tests, creating
- unit tests, running
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 3c5cb51232457a43200c8a71ace51cc4b8a63e02
ms.sourcegitcommit: 8e5b0106061bb43247373df33d0850ae68457f5e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88507981"
---
# <a name="run-a-unit-test-as-a-64-bit-process"></a>将单元测试作为 64 位进程运行

如果你有一台 64 位计算机，则可以作为 64 位进程来运行单元测试并捕获代码覆盖率信息。

## <a name="to-run-a-unit-test-as-a-64-bit-process"></a>将单元测试作为 64 位进程运行的具体步骤

1. 如果代码或测试是以 32 位/x86 形式编译，但现在希望将它们作为 64 位进程运行，请将它们重新编译为“Any CPU”  。

   ::: moniker range="vs-2017"
   或者，在 Visual Studio 2017 中，还可以将项目编译为 64 位  。
   ::: moniker-end

    > [!TIP]
    > 为了最大限度地提高灵活性，请使用“任何 CPU”  配置来编译测试项目。 然后，可以在 32 位和 64 位代理上运行。 除非要调用仅 64 位支持的代码，否则使用 64 位配置编译测试项目不具有任何优势。

2. 将单元测试设置为作为 64 位进程运行。

   ::: moniker range=">=vs-2019"
   在 Visual Studio 菜单中，选择“测试”，然后选择“AnyCPU 项目的处理器体系结构”   。 选择“x64”  ，将测试作为 64 位进程运行。
   ::: moniker-end
   ::: moniker range="vs-2017"
   在 Visual Studio 菜单中，依次选择“测试”、“测试设置”和“处理器体系结构”    。 选择“x64”  ，将测试作为 64 位进程运行。
   ::: moniker-end

   \- 或 -

   在 .runsettings 文件中指定 `<TargetPlatform>x64</TargetPlatform>`  。 此方法的一个优点是可以在不同文件中指定设置组，并在不同设置之间快速切换。 您还可以在解决方案之间复制设置。 有关详细信息，请参阅[使用 .runsettings 文件配置单元测试](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)。

## <a name="see-also"></a>请参阅

- [使用测试资源管理器运行单元测试](../test/run-unit-tests-with-test-explorer.md)
- [单元测试代码](../test/unit-test-your-code.md)
