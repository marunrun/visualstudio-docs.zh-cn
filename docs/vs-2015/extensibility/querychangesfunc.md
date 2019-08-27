---
title: QUERYCHANGESFUNC |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- QUERYCHANGESFUNC
helpviewer_keywords:
- QUERYCHANGESFUNC callback function
- QUERYCHANGESDATA structure
ms.assetid: 9d383e2c-eee1-4996-973a-0652d4c5951c
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 42f901fa31b3b682c7e19c98f5707adb3b4fb3f3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193846"
---
# <a name="querychangesfunc"></a>QUERYCHANGESFUNC
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

这是一个回调函数，用于通过[SccQueryChanges](../extensibility/sccquerychanges-function.md)操作枚举集合的文件的名称，并确定每个文件的状态。  
  
 `SccQueryChanges`函数提供一组文件和一个指向`QUERYCHANGESFUNC`回调。 源代码管理插件枚举给定的列表，并提供的列表中每个文件 （通过此回调） 的状态。  
  
## <a name="signature"></a>签名  
  
```cpp#  
typedef BOOL (*QUERYCHANGESFUNC)(  
   LPVOID pvCallerData,  
   QUERYCHANGESDATA * pChangesData  
);  
```  
  
## <a name="parameters"></a>参数  
 pvCallerData  
 [in]`pvCallerData`参数由调用方 (IDE) 传递给[SccQueryChanges](../extensibility/sccquerychanges-function.md)。 源代码管理插件应作出任何假设内容的此值。  
  
 pChangesData  
 [in]指向[QUERYCHANGESDATA 结构](#LinkQUERYCHANGESDATA)结构描述对文件的更改。  
  
## <a name="return-value"></a>返回值  
 IDE 将返回相应的错误代码：  
  
|值|描述|  
|-----------|-----------------|  
|SCC_OK|继续进行处理。|  
|SCC_I_OPERATIONCANCELED|停止处理。|  
|SCC_E_xxx|任何相应的 SCC 错误应停止处理。|  
  
## <a name="LinkQUERYCHANGESDATA"></a> QUERYCHANGESDATA 结构  
 每个文件中传递的结构如下所示：  
  
```cpp#  
struct QUERYCHANGESDATA_A  
{  
    DWORD  dwSize;  
    LPCSTR lpFileName;  
    DWORD  dwChangeType;  
    LPCSTR lpLatestName;  
};  
  
typedef struct QUERYCHANGESDATA_A QUERYCHANGESDATA;  
  
struct QUERYCHANGESDATA_W  
{  
    DWORD   dwSize;  
    LPCWSTR lpFileName;  
    DWORD   dwChangeType;  
    LPCWSTR lpLatestName;  
};  
```  
  
 dwSize  
 此结构 （以字节为单位） 的大小。  
  
 lpFileName  
 此项的原始文件名称。  
  
 dwChangeType  
 指示文件的状态代码：  
  
|代码|描述|  
|----------|-----------------|  
|`SCC_CHANGE_UNKNOWN`|无法判断所发生的更改。|  
|`SCC_CHANGE_UNCHANGED`|没有针对此文件的名称更改。|  
|`SCC_CHANGE_DIFFERENT`|文件使用不同的标识，但数据库中存在相同的名称。|  
|`SCC_CHANGE_NONEXISTENT`|在数据库中或本地文件不存在。|  
|`SCC_CHANGE_DATABASE_DELETED`|从数据库中删除的文件。|  
|`SCC_CHANGE_LOCAL_DELETED`|本地删除的文件，但该文件仍存在在数据库中。 如果这不能确定，则返回`SCC_CHANGE_DATABASE_ADDED`。|  
|`SCC_CHANGE_DATABASE_ADDED`|文件添加到数据库，但不存在本地。|  
|`SCC_CHANGE_LOCAL_ADDED`|文件数据库中不存在，并且是新的本地文件。|  
|`SCC_CHANGE_RENAMED_TO`|文件重命名或移动的数据库中`lpLatestName`。|  
|`SCC_CHANGE_RENAMED_FROM`|文件重命名或移动从数据库中`lpLatestName`; 如果这是过于昂贵而无法跟踪，请返回不同的标记，如`SCC_CHANGE_DATABASE_ADDED`。|  
  
 lpLatestName  
 此项的当前文件名称。  
  
## <a name="see-also"></a>请参阅  
 [通过 IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)   
 [SccQueryChanges](../extensibility/sccquerychanges-function.md)   
 [错误代码](../extensibility/error-codes.md)
