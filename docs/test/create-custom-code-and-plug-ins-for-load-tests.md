---
title: 为负载测试创建自定义代码和插件
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.dialog.recorderplugin
helpviewer_keywords:
- Web performance tests, plug-ins
- load tests, plug-ins
ms.assetid: 0c0fcc99-673b-4ea0-a268-0475f66e5cb6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7cd3dbd5e7aeb00c2de1a656c26db3a377b8ffe8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665108"
---
# <a name="create-custom-code-and-plug-ins-for-load-tests"></a>为负载测试创建自定义代码和插件

自定义插件使用你编写的并附加到负载测试或 Web 性能测试的代码。 可使用负载测试 API 和 Web 性能测试 API 为测试创建自定义插件以展开内置功能。 可以向负载测试添加多个插件。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="tasks"></a>任务

|任务|关联主题|
|-|-----------------------|
|**创建负载测试的自定义插件**：可使用负载测试 API 创建自定义插件，以向负载测试添加更多测试功能。|-   [如何：使用负载测试 API](../test/how-to-use-the-load-test-api.md)<br />-   [如何：创建负载测试插件](../test/how-to-create-a-load-test-plug-in.md)|
|**创建 Web 性能测试的自定义插件：** 可使用 Web 性能测试 API 创建自定义插件，以向 Web 性能测试（包括在请求级别上）添加更多测试功能。 还可以创建 Web 服务测试。<br /><br /> 此外，可以创建一个 Web 记录器插件，该插件可在记录 Web 性能测试后并在该测试显示在 Web 性能测试结果查看器中之前修改该测试。|-   [如何：使用 Web 性能测试 API](../test/how-to-use-the-web-performance-test-api.md)<br />-   [如何：创建 Web 性能测试插件](../test/how-to-create-a-web-performance-test-plug-in.md)<br />-   [如何：创建请求级插件](../test/how-to-create-a-request-level-plug-in.md)<br />-   [如何：创建 Web 服务测试](../test/how-to-create-a-web-service-test.md)<br />-   [如何：创建记录器插件](../test/how-to-create-a-recorder-plug-in.md)|
|**将 UI 功能添加到 Web 性能测试结果查看器：** 可以使用 Visual Studio 外接程序向 Web 性能测试结果查看器添加多个 UI 功能。|-   [如何：为 Web 性能测试结果查看器创建 Visual Studio 外接程序](../test/how-to-create-an-add-in-for-the-web-performance-test-results-viewer.md)|
|**创建自定义 HTTP 正文编辑器：** 可以创建自定义编辑器来编辑来自 Web 服务的二进制或字符串 http XML 响应。|-   [如何：为 Web 性能测试编辑器创建自定义 HTTP 正文编辑器](../test/how-to-create-a-custom-http-body-editor-for-the-web-performance-test-editor.md)|

## <a name="reference"></a>参考

<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin>

<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>

<xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>

<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin>

<xref:Microsoft.VisualStudio.TestTools.LoadTesting>

## <a name="see-also"></a>请参阅

- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [生成和运行编码的 Web 性能测试](../test/generate-and-run-a-coded-web-performance-test.md)