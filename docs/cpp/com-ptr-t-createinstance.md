---
title: _com_ptr_t::CreateInstance
ms.date: 11/04/2016
f1_keywords:
- _com_ptr_t::CreateInstance
helpviewer_keywords:
- CreateInstance method [C++]
ms.assetid: ab89b0e1-9da3-4784-a079-58b17340f111
ms.openlocfilehash: c4f6cd54b90ab5fab69f91df67a8bf60b0b658f8
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62399352"
---
# <a name="comptrtcreateinstance"></a>_com_ptr_t::CreateInstance

**Microsoft 专用**

创建一个对象的新实例`CLSID`或`ProgID`。

## <a name="syntax"></a>语法

```
HRESULT CreateInstance(
   const CLSID& rclsid,
   IUnknown* pOuter=NULL,
   DWORD dwClsContext = CLSCTX_ALL
) throw( );
HRESULT CreateInstance(
   LPCWSTR clsidString,
   IUnknown* pOuter=NULL,
   DWORD dwClsContext = CLSCTX_ALL
) throw( );
HRESULT CreateInstance(
   LPCSTR clsidStringA,
   IUnknown* pOuter=NULL,
   DWORD dwClsContext = CLSCTX_ALL
) throw( );
```

#### <a name="parameters"></a>参数

*rclsid*<br/>
`CLSID`的对象。

*clsidString*<br/>
由 Unicode 字符串，包含`CLSID`(从"**{**") 或`ProgID`。

*clsidStringA*<br/>
使用 ANSI 代码页，包含的多字节字符串`CLSID`(从"**{**") 或`ProgID`。

*dwClsContext*<br/>
运行可执行代码的上下文。

*pOuter*<br/>
未知的外部[聚合](../atl/aggregation.md)。

## <a name="remarks"></a>备注

这些成员函数调用 `CoCreateInstance` 来创建新的 COM 对象，然后查询此智能指针的接口类型。 生成的指针随后将封装在此 `_com_ptr_t` 对象内。 `Release` 调用以减少前面封装指针的引用计数。 此例程将返回 HRESULT，指示成功或失败。

- **CreateInstance (***rclsid* **，***dwClsContext***)** 创建给定的对象的新运行实例`CLSID`.

- **CreateInstance (***clsidString* **，***dwClsContext***)** 创建给定的对象的新运行实例Unicode 字符串包含`CLSID`(从"**{**") 或`ProgID`。

- **CreateInstance (***clsidStringA* **，***dwClsContext***)** 创建给定的对象的新运行实例多字节字符字符串包含`CLSID`(从"**{**") 或`ProgID`。 调用[MultiByteToWideChar](/windows/desktop/api/stringapiset/nf-stringapiset-multibytetowidechar)，其假定该字符串为中的 ANSI 代码页而不是 OEM 代码页。

**结束 Microsoft 专用**

## <a name="see-also"></a>请参阅

[_com_ptr_t 类](../cpp/com-ptr-t-class.md)