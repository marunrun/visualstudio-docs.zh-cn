---
title: Web 性能测试 API
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, using the API
- APIs, Web performance tests
ms.assetid: 93a6a1dd-663b-4ab5-8760-7d6b081561d3
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d22c1962727d22af965c879de3ae5fea6d4e54af
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72653302"
---
# <a name="how-to-use-the-web-performance-test-api"></a>如何：使用 Web 性能测试 API

可以为 Web 性能测试编写代码。 Web 性能测试 API 可用来创建编码 Web 性能测试、Web 性能测试插件、请求插件、请求、提取规则以及验证规则。 组成这些类型的类是此 API 中的核心类。 此 API 中的其他类型则用来支持创建 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTest>、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin>、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequest>、<xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule> 和 <xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule> 对象。 可使用 <xref:Microsoft.VisualStudio.TestTools.WebTesting> 命名空间创建自定义 Web 性能测试。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

还可以使用 Web 性能测试 API 通过编程方式来创建和保存声明性 Web 性能测试。 为此，可以使用 <xref:Microsoft.VisualStudio.TestTools.WebTesting.DeclarativeWebTest> 和 <xref:Microsoft.VisualStudio.TestTools.WebTesting.DeclarativeWebTestSerializer> 类。

> [!TIP]
> 可使用对象浏览器来检查 <xref:Microsoft.VisualStudio.TestTools.WebTesting> 命名空间。 Visual C# 和 Visual Basic 编辑器均为使用此命名空间中的类编写代码提供了 IntelliSense 支持。

还可以为负载测试创建插件。 有关详细信息，请参阅[如何：使用负载测试 API](../test/how-to-use-the-load-test-api.md) 以及[如何：创建负载测试插件](../test/how-to-create-a-load-test-plug-in.md)。

## <a name="to-use-the-webtesting-namespace"></a>使用 WebTesting 命名空间

1. 打开包含 Web 性能测试的 Web 性能和负载测试项目。

2. 向测试解决方案添加一个 Visual C# 或 Visual Basic 类库项目。

3. 在 Web 性能和负载测试项目中添加对类库项目的引用。

4. 在类库项目中添加对 Microsoft.VisualStudio.QualityTools.WebTestFramework DLL 的引用。

5. 在位于类库项目中的类文件中，为 `using` 命名空间添加 <xref:Microsoft.VisualStudio.TestTools.WebTesting> 语句。

6. 创建实现 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin> 接口的类。

7. 生成项目。

8. 使用“Web 性能测试编辑器”添加新 Web 性能测试插件：

    1. 选择工具栏上的“添加 Web 测试插件”。 

         随即显示“添加 Web 测试插件”对话框  。

    2. 在“选择插件”  下，选择 Web 性能测试插件类。

    3. 在“选定插件的属性”窗格中，设置要在运行时使用的插件的初始值  。

        > [!NOTE]
        > 可根据需要从插件中公开任意多个属性；只需将其设置为公共、可设置并属于 Integer、Boolean 或 String 等基本类型。 以后还可以使用“属性”窗口来编辑 Web 性能测试插件属性。

    4. 选择 **“确定”** 。

9. 运行该 Web 性能测试。

     有关 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin> 的实现示例，请参见[如何：创建 Web 性能测试插件](../test/how-to-create-a-web-performance-test-plug-in.md)。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TestTools.WebTesting>
- [为负载测试创建自定义代码和插件](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [如何：使用负载测试 API](../test/how-to-use-the-load-test-api.md)
- [如何：创建 Web 性能测试插件](../test/how-to-create-a-web-performance-test-plug-in.md)