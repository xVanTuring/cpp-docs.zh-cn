---
title: 编译器错误 C2753
ms.date: 11/04/2016
f1_keywords:
- C2753
helpviewer_keywords:
- C2753
ms.assetid: 92bfeeac-524a-4a8e-9a4f-fb8269055826
ms.openlocfilehash: e13c45cec99e60d8aec7dcc3db8e5a4813ea7de9
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62228778"
---
# <a name="compiler-error-c2753"></a>编译器错误 C2753

'*模板*： 部分专用化不能与主模板的参数列表匹配

如果模板自变量列表与匹配参数列表，编译器会将它视为同一个模板。 不允许两次定义同一个模板。

## <a name="example"></a>示例

下面的示例生成 C2753，并显示了如何修复此错误：

```cpp
// C2753.cpp
// compile with: cl /c C2753.cpp
template<class T>
struct A {};

template<class T>
struct A<T> {};   // C2753
// try the following line instead
// struct A<int> {};

template<class T, class U, class V, class W, class X>
struct B {};
```