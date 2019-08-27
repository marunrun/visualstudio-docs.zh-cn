---
title: 加密警告
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: d96723ea-a293-488d-b9db-adb437e50cdd
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 669b7806e01772e6a871b6c6a9bf47907cf9a5a4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62816583"
---
# <a name="cryptography-warnings"></a>加密警告
加密警告支持通过正确使用加密提高库和应用程序的安全性。 这些警告帮助防止程序中出现安全漏洞。 如果你禁用其中的某个警告，你应当在代码中清楚标出原因，同时将你的开发项目通知指定的安全负责人。

|规则|描述|
|----------|-----------------|
|[CA5350：请勿使用弱加密算法](../code-quality/ca5350-do-not-use-weak-cryptographic-algorithms.md)|出于多种原因，现今使用弱加密算法和哈希函数，但不应使用它们来保证保密性或它们所保护的数据的完整性。        当此规则在代码中找到 TripleDES、SHA1、或 RIPEMD160 算法时，此规则将触发。|
|[CA5351 不使用损坏的加密算法](../code-quality/ca5351-do-not-use-broken-cryptographic-algorithms.md)|损坏的加密算法不安全，强烈建议不要使用。 当此规则在代码中找到 MD5 哈希算法，或者 DES 或 RC2 加密算法时，此规则将触发。|