---
title: VSG_NODEFAULT_INSTANCE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 19c95b0d-9a4d-441f-9ed7-3acb39e67521
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 304576391b2287aee7567b3ccc2e4514ce5cb2e8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62848455"
---
# <a name="vsg_nodefault_instance"></a>VSG_NODEFAULT_INSTANCE
通过其存在状况定义是否提供 [VsgDbg 类](vsgdbg-class.md)的默认实例（它提供编程捕获接口）。

## <a name="syntax"></a>语法

```C++
#define VSG_NODEFAULT_INSTANCE
```

## <a name="value"></a>“值”
 通过其存在或缺失的预处理器符号决定是否提供 `VsgDbg` 类的默认实例。 如果定义此符号，则不提供 `VsgDbg` 类的默认实例；否则，将在程序运行前提供并初始化默认实例。

 通过具有全局范围的指针 `g_pVsgDbg` 提供编程捕获接口。

```cpp
VsgDbg *g_pVsgDbg;
```

## <a name="remarks"></a>备注
 默认实例通常足够，但要在 DLL 外部创建 D3D 设备后使用 DLL 内部的编程捕获接口，您必须创建并管理自己的 `VsgDbg` 类的实例。 如果您正通过此方式管理自己的编程捕获 API 的接口，请通过定义 `VSG_NODEFAULT_INSTANCE` 禁用默认实例来避免开销。

 如果未禁用默认实例，则它将在程序运行前自动进行初始化并在程序终止时自动销毁。 您不必显式初始化或取消初始化此实例。

 若要禁用默认实例，必须在将 `vsgcapture.h` 包含在程序中之前定义 `VSG_NODEFAULT_INSTANCE`。

## <a name="example"></a>示例
 此示例说明如何禁用默认实例：

```cpp
// Define VSG_NODEFAULT_INSTANCE before including vsgcapture.h
#define VSG_NODEFAULT_INSTANCE

#include <vsgcapture.h>
```
