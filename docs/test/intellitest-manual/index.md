---
title: IntelliTest 参考手册 | Microsoft 开发人员测试工具
ms.date: 05/02/2017
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest Reference Manual, IntelliTest
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: d7258549b242091737e14e00980447eb48d5e78b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62551588"
---
# <a name="intellitest-reference-manual"></a>IntelliTest 参考手册

## <a name="contents"></a>内容

* **[IntelliTest 概述](introduction.md)**
  - [IntelliTest 的 Hello World](introduction.md#the-hello-world-of-intellitest)
  - [限制](introduction.md#limitations)
    * [不确定性](introduction.md#nondeterminism)
    * [并发](introduction.md#concurrency)
    * [本机代码](introduction.md#native-code)
    * [平台](introduction.md#platform)
    * [语言](introduction.md#language)
    * [符号推理](introduction.md#symbolic-reasoning)
    * [不正确的堆栈跟踪](introduction.md#incorrect-stack-traces)
  - [其他阅读材料](introduction.md#further-reading)

* **[IntelliTest 入门](getting-started.md)**
  - [重要特性](getting-started.md#important-attributes)
  - [重要的静态帮助程序类](getting-started.md#helper-classes)

* **[测试生成](test-generation.md)**
  - [测试生成器](test-generation.md#test-generators)
  - [参数化单元测试](test-generation.md#parameterized-unit-testing)
  - [泛型参数化单元测试](test-generation.md#generic-parameterized)
  - [允许异常](test-generation.md#allowing-exceptions)
  - [测试内部类型](test-generation.md#internal-types)
  - [假设和断言](test-generation.md#assumptions-and-assertions)
  - [前提条件](test-generation.md#precondition)
  - [后置条件](test-generation.md#postcondition)
  - [测试失败](test-generation.md#test-failures)
  - [安装和卸载](test-generation.md#setup-teardown)
  - [其他阅读材料](test-generation.md#further-reading)

* **[输入生成](input-generation.md)**
  - [约束求解器](input-generation.md#constraint-solver)
  - [动态代码覆盖率](input-generation.md#dynamic-code-coverage)
  - [整数和浮点](input-generation.md#integers-and-floats)
  - [对象](input-generation.md#objects)
  - [实例化现有类](input-generation.md#existing-classes)
  - [可见性](input-generation.md#visibility)
  - [参数化模拟](input-generation.md#parameterized-mocks)
  - [结构](input-generation.md#structs)
  - [数组和字符串](input-generation.md#arrays-and-strings)
  - [获取其他输入](input-generation.md#additional-inputs)
  - [其他阅读材料](input-generation.md#further-reading)

* **[浏览边界](exploration-bounds.md)**
  - [MaxConstraintSolverTime](exploration-bounds.md#maxconstraintsolvertime)
  - [MaxConstraintSolverMemory](exploration-bounds.md#maxconstraintsolvermemory)
  - [MaxBranches](exploration-bounds.md#maxbranches)
  - [MaxCalls](exploration-bounds.md#maxcalls)
  - [MaxStack](exploration-bounds.md#maxstack)
  - [MaxConditions](exploration-bounds.md#maxconditions)
  - [MaxRuns](exploration-bounds.md#maxruns)
  - [MaxRunsWithoutNewTests](exploration-bounds.md#maxrunswithoutnewtests)
  - [MaxRunsWithUniquePaths](exploration-bounds.md#maxrunswithuniquepaths)
  - [MaxExceptions](exploration-bounds.md#maxexceptions)
  - [TestExcludePathBoundsExceeded](exploration-bounds.md#testexcludepathboundsexceeded)
  - [TestEmissionFilter](exploration-bounds.md#testemissionfilter)
  - [TestEmissionBranchHits](exploration-bounds.md#testemissionbranchhits)

* **[属性术语表](attribute-glossary.md)**
  - [PexAssumeNotNull](attribute-glossary.md#pexassumenotnull)
  - [PexClass](attribute-glossary.md#pexclass)
  - [PexGenericArguments](attribute-glossary.md#pexgenericarguments)
  - [PexMethod](attribute-glossary.md#pexmethod)
  - [PexExplorationAttributeBase](attribute-glossary.md#pexexplorationattributebase)
  - [PexAssemblySettings](attribute-glossary.md#pexassemblysettings)
  - [PexAssemblyUnderTest](attribute-glossary.md#pexassemblyundertest)
  - [PexInstrumentAssemblyAttribute](attribute-glossary.md#pexinstrumentassemblyattribute)
  - [PexUseType](attribute-glossary.md#pexusetype)
  - [PexAllowedException](attribute-glossary.md#pexallowedexception)
  - [PexAllowedExceptionFromAssembly](attribute-glossary.md#pexallowedexceptionfromassembly)
  - [PexAllowedExceptionFromType](attribute-glossary.md#pexallowedexceptionfromtype)
  - [PexAllowedExceptionFromTypeUnderTest](attribute-glossary.md#pexallowedexceptionfromtypeundertest)

* **[设置瀑布图](settings-waterfall.md)**

* **[静态帮助程序类](static-helper-classes.md)**
  - [PexAssume](static-helper-classes.md#pexassume)
  - [PexAssert](static-helper-classes.md#pexassert)
  - [PexChoose](static-helper-classes.md#pexchoose)
  - [PexObserve](static-helper-classes.md#pexobserve)
  - [PexSymbolicValue](static-helper-classes.md#pexsymbolicvalue)

* **[警告和错误](warnings-and-errors.md)**
  - [已超出 MaxBranches](warnings-and-errors.md#maxbranches-exceeded)
  - [已超出 MaxConstraintSolverTime](warnings-and-errors.md#maxconstraintsolvertime-exceeded)
  - [已超出 MaxConditions](warnings-and-errors.md#maxconditions-exceeded)
  - [已超出 MaxCalls](warnings-and-errors.md#maxcalls-exceeded)
  - [已超出 MaxStack](warnings-and-errors.md#maxstack-exceeded)
  - [已超出 MaxRuns](warnings-and-errors.md#maxruns-exceeded)
  - [已超出 MaxRunsWithoutNewTests](warnings-and-errors.md#maxrunswithoutnewtests-exceeded)
  - [无法具体化解决方案](warnings-and-errors.md#cannot-concretize-solution)
  - [需要帮助来构造对象](warnings-and-errors.md#help-construct)
  - [需要帮助来查找类型](warnings-and-errors.md#help-types)
  - [猜测的可用类型](warnings-and-errors.md#usable-type-guessed)
  - [浏览期间的意外故障](warnings-and-errors.md#unexpected-exploration)
  - [TargetInvocationException](warnings-and-errors.md#targetinvocationexception)
  - [已调用未检测的方法](warnings-and-errors.md#uninstrumented-method-called)
  - [已调用外部方法](warnings-and-errors.md#external-method-called)
  - [已调用无法检测的方法](warnings-and-errors.md#uninstrumentable-method-called)
  - [可测试性问题](warnings-and-errors.md#testability-issue)
  - [限制](warnings-and-errors.md#limitation)
  - [观察到调用不匹配](warnings-and-errors.md#observed-call-mismatch)
  - [存储在静态字段中的值](warnings-and-errors.md#value-static-field)

## <a name="got-feedback"></a>是否获得反馈？

在[开发人员社区](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)上发布想法和功能请求。