---
title: 复制（编程捕获）| Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 30ec235a-0abb-44b9-8852-61bc9e67ce22
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3a888605cfae6b5430782defd198f83988c31870
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62895949"
---
# <a name="copy-programmatic-capture"></a>复制（编程捕获）
将活动图形日志 (.vsglog) 文件的内容复制到新文件。

## <a name="syntax"></a>语法

```C++
void Copy(
  wchar_t const * szNewVSGLog
);
```

#### <a name="parameters"></a>参数
 `szNewVSGLog` 新图形日志文件的文件名。

## <a name="remarks"></a>备注
 若要将图形信息复制到新文件，您必须已捕获一些图形信息；否则，不会执行任何操作。