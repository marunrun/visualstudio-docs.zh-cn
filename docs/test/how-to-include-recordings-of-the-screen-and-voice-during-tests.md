---
title: 在测试期间录制屏幕和语音
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- test settings, recording desktop video
ms.assetid: 2cefe8c2-430a-4cb4-bbe0-f3edb2e5bc03
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 572b3132056ebed1d26c983fdc4024d2ddc51a82
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72653526"
---
# <a name="how-to-include-recordings-of-the-screen-and-voice-during-tests-using-test-settings"></a>如何：使用测试设置在测试期间包括屏幕和语音录制

通过 Visual Studio 中的配置编辑器，可以配置录制运行测试的用户的屏幕和语音的诊断数据适配器。 此诊断数据适配器将在测试期间保存桌面会话的屏幕和语音录制。 该录制与测试结果一起保存或者可将其附加到 Bug。 其他团队成员可以使用该录制隔离难以重现的应用程序缺陷。

> [!WARNING]
> 屏幕和语音录制不支持多监视器配置。

屏幕和语音录制器可用于手动测试或自动测试。 例如，如果您远程运行编码的 UI 测试，可能希望录制桌面以便在运行编码的 UI 测试时可以查看该测试。 有关如何远程捕获屏幕和语音录制的详细信息，请参阅[如何：设置测试代理以运行与桌面交互的测试](../test/how-to-set-up-your-test-agent-to-run-tests-that-interact-with-the-desktop.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-configure-screen-and-voice-recording-for-your-test-settings"></a>为测试设置配置屏幕和语音录制

1. 打开要为录制屏幕和语音配置的测试设置。 有关详细信息，请参阅[在测试时收集诊断数据 (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts) 或[使用测试设置收集诊断信息](../test/collect-diagnostic-information-using-test-settings.md)。

2. 在测试设置中，选择要用于录制屏幕和语音的“角色”  。

    > [!NOTE]
    > 对于手动测试和自动测试，这将为运行测试的计算机。

3. 选择“屏幕和语音录制器”，然后选择“配置”   。

     “配置诊断数据适配器 - 屏幕和语音录制器”对话框随即出现  。

     ![视频配置](../test/media/testsettingvideoconfiggdr.png)

4. （可选）选择“启用语音录制”来捕获您录制的音频内容  。

5. （可选）选中“如果测试用例通过则保存录制内容”旁边的复选框，以指定为失败的测试和通过的测试保存屏幕和语音录制  。

    > [!WARNING]
    > 如果选择“如果测试用例通过则保存录制内容”，则该录制将与测试结果一起存储，这将占用服务器上的存储空间  。 可使用“测试附件清理器”工具来清理这些附件  。

6. 在“屏幕录制质量”下，配置以下下拉列表选项  ：

    1. **帧速率：** 指定要在屏幕和语音录制中使用的每秒帧数。 默认值为 4 帧/每秒。 可指定介于 2 和 20 之间的值。

    2. **比特率：** 指定要在屏幕和语音录制器中使用的每秒 KB 数。 默认值为 512。 可指定介于 512 和 10,000 之间的值。

    3. **品质 (1-100)：** 可以通过选择介于 1 和 100 之间的范围来指定屏幕和语音录制的品质。 默认值为 50（中等范围）。

7. 选择 **“确定”** 。 现在已为测试设置配置和保存了诊断跟踪收集器设置。

    > [!TIP]
    > 若要重置此诊断数据适配器的配置，请为 Visual Studio 选择“重置为默认配置”，并为 Microsoft 测试管理器选择“重置为默认值”   。

## <a name="see-also"></a>请参阅

- [在测试时收集诊断数据 (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts)
- [在手动测试中收集诊断数据 (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)
- [使用测试设置收集诊断信息](../test/collect-diagnostic-information-using-test-settings.md)
- [运行手动测试 (Azure Test Plans)](/azure/devops/test/run-manual-tests?view=vsts)