---
title: span 类 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::span
helpviewer_keywords:
- Concurrency::diagnostic::span class
ms.assetid: 527826a8-2590-43ad-b907-7bc0b7288e92
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8d8f31d24dc6c6c2ea20b50c9bf8af1cb4a9f9af
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62979752"
---
# <a name="span-class"></a>span 类
定义应用程序的一个阶段。

## <a name="syntax"></a>语法

```cpp
class span;
```

## <a name="members"></a>成员

### <a name="public-constructors"></a>公共构造函数

|“属性”|描述|
|----------|-----------------|
|[span::span 构造函数](../profiling/span-span-constructor.md)|初始化 `span` 类的新实例。|
|[span::~span 析构函数](../profiling/span-tilde-span-destructor.md)|销毁 `span` 对象并释放其资源。|

## <a name="inheritance-hierarchy"></a>继承层次结构
 `span`

## <a name="requirements"></a>要求
 **Header:** *cvmarkersobj.h*

 **命名空间：** Concurrency::diagnostic

## <a name="see-also"></a>请参阅
- [diagnostic 命名空间](../profiling/diagnostic-namespace.md)