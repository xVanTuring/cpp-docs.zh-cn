---
title: '&lt;allocators&gt; 宏'
ms.date: 11/04/2016
f1_keywords:
- allocators/std::ALLOCATOR_DECL
- allocators/std::CACHE_CHUNKLIST
- allocators/std::CACHE_FREELIST
- allocators/std::CACHE_SUBALLOC
- allocators/std::SYNC_DEFAULT
ms.assetid: 9cb5ee07-1ff9-4594-ae32-3c8c6efb511a
helpviewer_keywords:
- std::ALLOCATOR_DECL [C++]
- std::CACHE_CHUNKLIST [C++]
- std::CACHE_FREELIST [C++]
- std::CACHE_SUBALLOC [C++]
- std::SYNC_DEFAULT [C++]
ms.openlocfilehash: 736e587a41fa1006801dcf6930b33ee434c9a5ea
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62179206"
---
# <a name="ltallocatorsgt-macros"></a>&lt;allocators&gt; 宏

||||
|-|-|-|
|[ALLOCATOR_DECL](#allocator_decl)|[CACHE_CHUNKLIST](#cache_chunklist)|[CACHE_FREELIST](#cache_freelist)|
|[CACHE_SUBALLOC](#cache_suballoc)|[SYNC_DEFAULT](#sync_default)|

## <a name="allocator_decl"></a>  ALLOCATOR_DECL

生成一个分配器模板类。

```cpp
#define ALLOCATOR_DECL(cache, sync, name) <alloc_template>
```

### <a name="remarks"></a>备注

宏生成一个模板定义 `template <class Type> class name {.....}` 和一个专用化 `template <> class name<void> {.....}`，它们一同定义使用同步筛选器 `sync` 和缓存类型为 `cache` 的分配器模板类。

对于可以编译重新绑定的编译器，其生成的模板定义如下所示：

```cpp
struct rebind
   {    /* convert a name<Type> to a name<Other> */
   typedef name<Other> other;
   };
```

对于无法编译重新绑定的编译器，其生成的模板定义如下所示：

```cpp
template <class Type<class name
    : public stdext::allocators::allocator_base<Type,
    sync<stdext::allocators::rts_alloc<cache>>>
{
public:
    name() {}
    template <class Other>
    name(const name<Other>&) {}
    template <class Other>
    name& operator= (const name<Other>&)
    {
        return *this;
    }
};
```

## <a name="cache_chunklist"></a>  CACHE_CHUNKLIST

生成 `stdext::allocators::cache_chunklist<sizeof(Type)>`。

```cpp
#define CACHE_CHUNKLIST <cache_class>
```

### <a name="remarks"></a>备注

## <a name="cache_freelist"></a>  CACHE_FREELIST

生成 `stdext::allocators::cache_freelist<sizeof(Type), max>`。

```cpp
#define CACHE_FREELIST(max) <cache_class>
```

### <a name="remarks"></a>备注

## <a name="cache_suballoc"></a>  CACHE_SUBALLOC

生成 `stdext::allocators::cache_suballoc<sizeof(Type)>`。

```cpp
#define CACHE_SUBALLOC <cache_class>
```

### <a name="remarks"></a>备注

## <a name="sync_default"></a>  SYNC_DEFAULT

生成同步筛选器。

```cpp
#define SYNC_DEFAULT <sync_template>
```

### <a name="remarks"></a>备注

如果编译器支持编译单线程和多线程应用程序，则对于单线程应用程序，宏生成 `stdext::allocators::sync_none`；在所有其他情况下生成 `stdext::allocators::sync_shared`。

## <a name="see-also"></a>请参阅

[\<allocators>](../standard-library/allocators-header.md)<br/>
