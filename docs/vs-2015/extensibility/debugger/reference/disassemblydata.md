---
title: DisassemblyData |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- DisassemblyData
helpviewer_keywords:
- DisassemblyData structure
ms.assetid: 10e70aa7-9381-40d3-bdd1-d2cad78ef16c
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ea21b4ae9e6e852efcc3625dc3af24478bd88155
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198821"
---
# <a name="disassemblydata"></a>DisassemblyData
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

描述用于显示 (IDE) 的集成开发环境的一种反汇编说明。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct tagDisassemblyData {   
   DISASSEMBLY_STREAM_FIELDS dwFields;  
   BSTR                      bstrAddress;  
   BSTR                      bstrAddressOffset;  
   BSTR                      bstrCodeBytes;  
   BSTR                      bstrOpcode;  
   BSTR                      bstrOperands;  
   BSTR                      bstrSymbol;  
   UINT64                    uCodeLocationId;  
   TEXT_POSITION             posBeg;  
   TEXT_POSITION             posEnd;  
   BSTR                      bstrDocumentUrl;  
   DWORD                     dwByteOffset;  
   DISASSEMBLY_FLAGS         dwFlags;  
} DisassemblyData;  
```  
  
```csharp  
public struct DisassemblyData {   
   public uint          dwFields;  
   public string        bstrAddress;  
   public string        bstrAddressOffset;  
   public string        bstrCodeBytes;  
   public string        bstrOpcode;  
   public string        bstrOperands;  
   public string        bstrSymbol;  
   public ulong         uCodeLocationId;  
   public TEXT_POSITION posBeg;  
   public TEXT_POSITION posEnd;  
   public string        bstrDocumentUrl;  
   public uint          dwByteOffset;  
   public uint          dwFlags;  
};  
```  
  
## <a name="members"></a>成员  
 `dwFields`  
 用于指定填充了哪些字段的 [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md) 常数。  
  
 `bstrAddress`  
 从某个起点开始的偏移量 (通常是关联函数) 的开头。  
  
 `bstrCodeBytes`  
 此指令的代码字节。  
  
 `bstrOpcode`  
 此指令的操作码。  
  
 `bstrOperands`  
 此指令的操作数。  
  
 `bstrSymbol`  
 与该地址关联的符号名称（如果有） (公共符号、标签等) 上。  
  
 `uCodeLocationId`  
 此反汇编行的代码位置标识符。 如果一个行的代码上下文地址大于另一个行的代码上下文地址，则第一个行的反汇编代码位置标识符也将大于第二个代码位置的标识符。  
  
 `posBeg`  
 与开始反汇编数据的文档中的位置相对应的 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 。  
  
 `posEnd`  
 与反汇编数据在文档中的位置相对应的 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 。  
  
 `bstrDocumentUrl`  
 对于可以表示为文件名的文本文档，该 `bstrDocumentUrl` 字段将使用格式以可找到源的文件名填充 `file://file name` 。  
  
 对于不能表示为文件名的文本文档， `bstrDocumentUrl` 是文档的唯一标识符，调试引擎必须实现 [GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md) 方法。  
  
 此字段还可以包含与校验和有关的其他信息。 有关详细信息，请参阅备注。  
  
 `dwByteOffset`  
 指令从代码行开头开始的字节数。  
  
 `dwFlags`  
 指定哪些标志处于活动状态的 [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md) 常数。  
  
## <a name="remarks"></a>备注  
 每个 `DisassemblyData` 结构都描述了一个反汇编指令。 从 [Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md) 方法返回这些结构的数组。  
  
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)结构仅用于基于文本的文档。 此指令的源代码范围仅针对从语句或行生成的第一个指令填写，例如，在时为 `dwByteOffset == 0` 。  
  
 对于非文本文档，可以从代码中获取文档上下文，并且 `bstrDocumentUrl` 字段应为 null 值。 如果 `bstrDocumentUrl` 字段与 `bstrDocumentUrl` 上一个数组元素中的字段相同 `DisassemblyData` ，则将设置 `bstrDocumentUrl` 为 null 值。  
  
 如果 `dwFlags` 字段 `DF_DOCUMENT_CHECKSUM` 设置了标志，则附加的校验和信息将在字段指向的字符串之后 `bstrDocumentUrl` 。 具体而言，在空字符串终止符之后，会出现一个标识校验和算法的 GUID，该 GUID 后面跟着一个4字节值，指示校验和中的字节数，然后再后跟校验和字节。 请参阅本主题中的示例，了解如何在中对此字段进行编码和解码 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 。  
  
## <a name="example"></a>示例  
 `bstrDocumentUrl`如果设置了标志，则字段可以包含字符串以外的其他信息 `DF_DOCUMENT_CHECKSUM` 。 创建和读取此编码字符串的过程在中非常简单 [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] 。 但是，在中 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] ，这也是另一回事。 对于好奇的用户，下面的示例演示了一种从中创建编码字符串的方法， [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 以及一种解码中编码字符串的方法 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 。  
  
```csharp  
using System;  
using System.Runtime.InteropServices;  
  
namespace MyNamespace  
    class MyClass  
    {  
        string EncodeData(string documentString,  
                          Guid checksumGuid,  
                          byte[] checksumData)  
        {  
            string returnString = documentString;  
  
            if (checksumGuid == null || checksumData == null)  
            {  
                // Nothing more to do. Just return the string.  
                return returnString;  
            }  
  
            returnString += '\0'; // separating null value  
  
            // Add checksum GUID to string.  
            byte[] guidDataArray  = checksumGuid.ToByteArray();  
            int    guidDataLength = guidDataArray.Length;  
            IntPtr pBuffer        = Marshal.AllocCoTaskMem(guidDataLength);  
            for (int i = 0; i < guidDataLength; i++)  
            {  
                Marshal.WriteByte(pBuffer, i, guidDataArray[i]);  
            }  
            // Copy guid data bytes to string as wide characters.  
            // Assumption: sizeof(char) == 2.  
            for (int i = 0; i < guidDataLength; i++)  
            {  
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));  
            }  
  
            // Add checksum count (a 32-bit value).  
            Int32 checksumCount = checksumData.Length;  
            Marshal.StructureToPtr(checksumCount, pBuffer, true);  
            for (int i = 0; i < sizeof(Int32) / sizeof(char); i++)  
            {  
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));  
            }  
  
            // Add checksum data.  
            pBuffer = Marshal.AllocCoTaskMem(checksumCount);  
            for (int i = 0; i < checksumCount; i++)  
            {  
                Marshal.WriteByte(pBuffer, i, checksumData[i]);  
            }  
            for (int i = 0; i < checksumCount / sizeof(char); i++)  
            {  
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));  
            }  
            Marshal.FreeCoTaskMem(pBuffer);  
  
            return returnString;  
        }  
  
        void DecodeData(    string encodedString,  
                        out string documentString,  
                        out Guid   checksumGuid,  
                        out byte[] checksumData)  
       {  
           documentString = String.Empty;  
           checksumGuid = Guid.Empty;  
           checksumData = null;  
  
           IntPtr pBuffer = Marshal.StringToBSTR(encodedString);  
           if (null != pBuffer)  
           {  
               int bufferOffset = 0;  
  
               // Parse string out.  String is assumed to be Unicode.  
               documentString = Marshal.PtrToStringUni(pBuffer);  
               bufferOffset += (documentString.Length + 1) * sizeof(char);  
  
               // Parse Guid out.  
               // Read guid bytes from buffer and store in temporary  
               // buffer that contains only the guid bytes. Then the  
               // Marshal.PtrToStructure() can work properly.  
               byte[] guidDataArray  = checksumGuid.ToByteArray();  
               int    guidDataLength = guidDataArray.Length;  
               IntPtr pGuidBuffer    = Marshal.AllocCoTaskMem(guidDataLength);  
               for (int i = 0; i < guidDataLength; i++)  
               {  
                   Marshal.WriteByte(pGuidBuffer, i,  
                                     Marshal.ReadByte(pBuffer, bufferOffset + i);  
               }  
               bufferOffset += guidDataLength;  
               checksumGuid = (Guid)Marshal.PtrToStructure(pGuidBuffer, typeof(Guid));  
               Marshal.FreeCoTaskMem(pGuidBuffer);  
  
              // Parse out the number of checksum data bytes (always 32-bit value).  
              int dataCount = Marshal.ReadInt32(pBuffer, bufferOffset);  
              bufferOffset += sizeof(Int32);  
  
              // Parse out the checksum data.  
              checksumData = new byte[dataCount];  
              for (int i = 0; i < dataCount; i++)  
              {  
                  checksumData[i] = Marshal.ReadByte(pBuffer, bufferOffset + i);  
              }  
           }  
       }  
    }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [读取](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)   
 [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)   
 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)   
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)   
 [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
