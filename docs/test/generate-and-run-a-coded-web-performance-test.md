---
title: 编码的 Web 性能测试
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, walkthroughs
- Web performance tests, creating
- code, Web performance tests
- Web performance tests, coded
ms.assetid: 169e48f9-52fd-4d0b-83d9-54913bde506b
dev_langs:
- CSharp
- VB
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4297f60c74e32b904d7c36912a8377d33f23ebdf
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75589573"
---
# <a name="generate-and-run-a-coded-web-performance-test"></a>生成和运行编码的 Web 性能测试

通过浏览 Web 应用记录 Web 性能测试。 测试包含在负载测试中，用于测量多个用户压力下的 Web 应用程序的性能。 可以将 Web 性能测试转换为基于代码的脚本（你可以像对待任何其他源代码一样对其进行编辑和自定义）。 例如，可以添加循环和分支构造。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="generate-a-coded-web-performance-test"></a>生成编码的 Web 性能测试

1. 如果尚未创建 Web 性能测试，请参阅[记录 Web 性能测试](/azure/devops/test/load-test/run-performance-tests-app-before-release#create-a-web-performance-and-load-test-project)。

2. 生成编码的测试。

     ![生成编码的 Web 性能测试](../test/media/web_test_coded_generate.png)

3. 为测试命名。

     ![输入编码 Web 性能测试的名称](../test/media/web_test_coded_generate_nametest.png)

     新编码的测试将在代码编辑器中打开。

     将在 Visual Basic 或 Visual C# 中生成代码，具体取决于你向解决方案添加了哪个 Web 性能和负载测试项目模板。

     ![新的编码的测试将在代码编辑器中打开](../test/media/web_test_coded_generate_opencodeeditor.png)

     你可在代码中看到 C# 中的 GetRequestEnumerator() 方法或 Visual Basic 中的 Run() 方法包括每个验证规则和已记录测试中的 Web 请求。

4. 若要展示添加一些简单代码的操作，请向下滚动到所选方法的末尾，并在最后一个 Web 请求的代码后面添加以下代码：

    ```c#
    if (DateTime.Today.DayOfWeek == DayOfWeek.Wednesday)
    {
        WebTestRequest customRequest = new WebTestRequest("http://weather.msn.com/");
        yield return customRequest;
    }
    else
    {
        WebTestRequest customRequest = new WebTestRequest("https://msdn.microsoft.com/");
        yield return customRequest;
    }
    ```

    ```vb
    If DateTime.Today.DayOfWeek = DayOfWeek.Wednesday Then
        Dim customRequest As WebTestRequest = New WebTestRequest("http://weather.msn.com/")
        MyBase.Send(customRequest)
    Else
        Dim customRequest As WebTestRequest = New WebTestRequest("https://msdn.microsoft.com/")
        MyBase.Send(customRequest)
    End If
    ```

5. 生成解决方案来验证你的自定义代码是否编译。

6. 运行测试。

     ![运行编码的 Web 性能测试](../test/media/web_test_coded_generate_run.png)

     并且因为运行该测试的时间碰巧是星期三…

     ![编码 Web 性能测试结果查看器](../test/media/web_test_coded_generate_results.png)

## <a name="qa"></a>问题解答

### <a name="q-can-i-run-more-than-one-test-at-a-time"></a>问：是否能一次运行多个测试？
**答：** 能，请使用“解决方案资源管理器”  中的右键单击菜单（关联菜单）。

### <a name="q-should-i-add-a-data-source-before-or-after-i-generate-a-coded-test"></a>问：我是否应在生成编码的测试之前和之后添加数据源？
**答：** 可在你生成编码的测试之前更轻松地添加[数据源](../test/add-a-data-source-to-a-web-performance-test.md)，因为将为你自动生成代码。

当你使用数据源运行编码测试时，你可能看到以下错误消息：

**无法运行测试\<测试名称 > 代理\<计算机名 >：对象引用未设置为某个对象的实例。**

发生此错误的原因是，你有为测试类定义的 DataSourceAttribute，而没有相应的 DataBindingAttribute。 若要纠正此错误，请添加适当的 DataBindingAttribute 并将其删除，或从代码中将其注释掉。

### <a name="q-should-i-add-validation-and-extraction-rules-before-or-after-i-generate-a-coded-test"></a>问：我是否应在生成编码的测试之前和之后添加验证和提取规则？
**答：** 在你生成编码的测试之前，可以更轻松地添加验证规则和提取规则；但是，我们建议你使用[编码的 UI 测试](../test/use-ui-automation-to-test-your-code.md)来进行验证。
