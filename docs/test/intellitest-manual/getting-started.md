---
title: IntelliTest 简介
ms.date: 05/02/2017
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest, Get started
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 113233c985053cfe838f385a36ec59cc211bfcb9
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591653"
---
# <a name="get-started-with-microsoft-intellitest"></a>Microsoft IntelliTest 入门

* 如果首次使用 IntelliTest：
  * 观看[第 9 频道视频](https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Intellitest)
  * 阅读 [MSDN 杂志的概述](https://msdn.microsoft.com/magazine/dn904672.aspx)
  * 阅读[文档](../../test/generate-unit-tests-for-your-code-with-intellitest.md)
* 在 [Stack Overflow](https://stackoverflow.com/questions/tagged/intellitest) 上提问
* 阅读此参考手册的其余部分
* 打印此页以供快速参考

## <a name="important-attributes"></a>重要属性

* [PexClass](attribute-glossary.md#pexclass) 标记包含 PUT  的类型
* [PexMethod](attribute-glossary.md#pexmethod) 标记 PUT 
* [PexAssumeNotNull](attribute-glossary.md#pexassumenotnull) 标记非 null 参数

```csharp
using Microsoft.Pex.Framework;

[..., PexClass(typeof(Foo))]
public partial class FooTest {
    [PexMethod]
    public void Bar([PexAssumeNotNull]Foo target, int i) {
        target.Bar(i);
    }
}
```

* [PexAssemblyUnderTest](attribute-glossary.md#pexassemblyundertest) 将测试项目绑定到一个项目
* [PexInstrumentAssembly](attribute-glossary.md#pexinstrumentassemblyattribute) 指定要检测的程序集

```csharp
[assembly: PexAssemblyUnderTest("MyAssembly")] // also instruments "MyAssembly"
[assembly: PexInstrumentAssembly("Lib")]
```

## <a name="helper-classes"></a> 重要的静态帮助程序类

* [PexAssume](static-helper-classes.md#pexassume) 评估假设（输入筛选）
* [PexAssert](static-helper-classes.md#pexassert) 评估断言
* [PexChoose](static-helper-classes.md#pexchoose) 生成新选项（其他输入）
* [PexObserve](static-helper-classes.md#pexobserve) 将实时值记录到生成的测试中

```csharp
[PexMethod]
void StaticHelpers(Foo target) {
    PexAssume.IsNotNull(target);

    int i = PexChoose.Value<int>("i");
    string result = target.Bar(i);

    PexObserve.ValueForViewing<string>("result", result);
    PexAssert.IsNotNull(result);
}
```

## <a name="got-feedback"></a>是否获得反馈？

在[开发人员社区](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)上发布想法和功能请求。
