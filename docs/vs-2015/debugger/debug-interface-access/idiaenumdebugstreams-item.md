---
title: IDiaEnumDebugStreams::Item | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams::Item method
ms.assetid: 6b388fe1-eabc-4720-9d59-dc09b0ceaeac
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e7559ffe33c5e53ef882962d04e0e6f69b49a6e6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68182583"
---
# <a name="idiaenumdebugstreamsitem"></a>IDiaEnumDebugStreams::Item
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索调试流通过索引或名称。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Item (   
   VARIANT                   index,  
   IDiaEnumDebugStreamData** stream  
);  
```  
  
#### <a name="parameters"></a>参数  
 索引  
 [in]要检索的索引或调试流的名称。 如果使用整数变量，则它必须是介于 0 到`count`-1，其中`count`与返回的[idiaenumdebugstreams:: Get_count](../../debugger/debug-interface-access/idiaenumdebugstreams-get-count.md)方法。  
  
 流  
 [out]返回[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)对象，表示指定的调试流。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="example"></a>示例  
  
```cpp#  
IDiaEnumDebugStreamData *GetStreamData(IDiaEnumDebugStreams *pStreamList,  
                                       LONG whichStream)  
{  
    IDiaEnumDebugStreamData *pStreamData = NULL;  
    if (pStreamList != NULL)  
    {  
        LONG numStreams = 0;  
        if (pStreamList->get_count(&numStreams) == S_OK &&  
            whichStream >= 0 && whichStream < numStreams)  
        {  
            VARIANT vIndex;  
            vIndex.vt   = VT_I4;  
            vIndex.lVal = whichStream;  
            if (pStreamList->Item(vIndex,&pStreamData) != S_OK)  
            {  
                 std::cerr << "Error retrieving stream " << whichStream << std::endl;  
            }  
        }  
    }  
    return(pStreamData);  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)   
 [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)
