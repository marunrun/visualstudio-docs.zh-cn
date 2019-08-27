---
title: DisassemblyData |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DisassemblyData
helpviewer_keywords:
- DisassemblyData structure
ms.assetid: 10e70aa7-9381-40d3-bdd1-d2cad78ef16c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: edc91cf8599a8591b70d14c49611ff64d5e957e6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318219"
---
# <a name="disassemblydata"></a>DisassemblyData
描述一个反汇编指令的集成的开发环境 (IDE) 来显示。

## <a name="syntax"></a>语法

```cpp
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
`dwFields`\
[DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)常量，它指定哪些字段填写。

`bstrAddress`\
为从某个起点 （通常关联函数的开头） 的偏移量地址。

`bstrCodeBytes`\
此指令代码字节。

`bstrOpcode`\
此指令的操作码。

`bstrOperands`\
此指令的操作数。

`bstrSymbol`\
与地址 （公共符号、 标签等） 关联的符号名称，如果有的话。

`uCodeLocationId`\
反汇编此行代码位置标识符。 如果同一行的代码上下文地址大于另一个代码上下文地址，然后反汇编的代码位置标识符的第一个也将大于第二个的代码位置标识符。

`posBeg`\
[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) ，它对应于文档中反汇编数据开始处的位置。

`posEnd`\
[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) ，它对应于文档中的反汇编数据的结束位置的位置。

`bstrDocumentUrl`\
文本文档，可以表示为文件的名称，`bstrDocumentUrl`字段中填写的文件名，其中可以找到源，使用格式`file://file name`。

不能作为文件的名称，表示文本文档`bstrDocumentUrl`是该文档的唯一标识符和调试引擎必须实现[GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)方法。

此字段还可以包含有关校验和的其他信息。 有关详细信息，请参阅备注。

`dwByteOffset`\
指令是从代码行的开头的字节数。

`dwFlags`\
[DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)常量，它指定的标志处于活动状态。

## <a name="remarks"></a>备注
每个`DisassemblyData`结构描述的反汇编的一条指令。 从返回这些结构的数组[读取](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)方法。

[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)结构用于基于文本的文档。 此指令的源的代码范围填充此值仅从语句或行，例如生成的第一个指令，当`dwByteOffset == 0`。

为非文本的文档，可以从代码中，获取文档上下文和`bstrDocumentUrl`字段应为 null 值。 如果`bstrDocumentUrl`字段是与相同`bstrDocumentUrl`字段中的上一个`DisassemblyData`数组元素，则设置`bstrDocumentUrl`为 null 值。

如果`dwFlags`字段具有`DF_DOCUMENT_CHECKSUM`标志设置，然后指向的字符串之后附加校验和信息`bstrDocumentUrl`字段。 具体而言，null 字符串终止符后那里遵循标识校验和算法后又跟一个 4 字节值，该值校验和中的字节数和依次后跟的校验和字节的 GUID。 有关如何进行编码和解码此字段中的，请参阅本主题中的示例[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)]。

## <a name="example"></a>示例
`bstrDocumentUrl`字段可以包含除字符串以外的其他信息，如果`DF_DOCUMENT_CHECKSUM`设置标志。 创建和读取此编码的字符串的过程非常简单中[!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)]。 但是，在[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)]，它是另外一回事。 对于那些大家的好奇心，下面的示例演示一种方法创建从编码的字符串[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)]和解码已编码的字符串中的一种方法[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)]。

```csharp
using System;
using System.Runtime.InteropServices;

namespace MyNamespace
{
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
            for (int i = 0; i < guidDataLength / sizeof(char); i++)
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

                // Parse string out. String is assumed to be Unicode.
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
                                      Marshal.ReadByte(pBuffer, bufferOffset + i));
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

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)
- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
