---
title: basic_ios 类
ms.date: 11/04/2016
f1_keywords:
- ios/std::basic_ios
- ios/std::basic_ios::char_type
- ios/std::basic_ios::int_type
- ios/std::basic_ios::off_type
- ios/std::basic_ios::pos_type
- ios/std::basic_ios::traits_type
- ios/std::basic_ios::bad
- ios/std::basic_ios::clear
- ios/std::basic_ios::copyfmt
- ios/std::basic_ios::eof
- ios/std::basic_ios::exceptions
- ios/std::basic_ios::fail
- ios/std::basic_ios::fill
- ios/std::basic_ios::good
- ios/std::basic_ios::imbue
- ios/std::basic_ios::init
- ios/std::basic_ios::move
- ios/std::basic_ios::narrow
- ios/std::basic_ios::rdbuf
- ios/std::basic_ios::rdstate
- ios/std::basic_ios::set_rdbuf
- ios/std::basic_ios::setstate
- ios/std::basic_ios::swap
- ios/std::basic_ios::tie
- ios/std::basic_ios::widen
- ios/std::basic_ios::explicit operator bool
helpviewer_keywords:
- std::basic_ios [C++]
- std::basic_ios [C++], char_type
- std::basic_ios [C++], int_type
- std::basic_ios [C++], off_type
- std::basic_ios [C++], pos_type
- std::basic_ios [C++], traits_type
- std::basic_ios [C++], bad
- std::basic_ios [C++], clear
- std::basic_ios [C++], copyfmt
- std::basic_ios [C++], eof
- std::basic_ios [C++], exceptions
- std::basic_ios [C++], fail
- std::basic_ios [C++], fill
- std::basic_ios [C++], good
- std::basic_ios [C++], imbue
- std::basic_ios [C++], init
- std::basic_ios [C++], move
- std::basic_ios [C++], narrow
- std::basic_ios [C++], rdbuf
- std::basic_ios [C++], rdstate
- std::basic_ios [C++], set_rdbuf
- std::basic_ios [C++], setstate
- std::basic_ios [C++], swap
- std::basic_ios [C++], tie
- std::basic_ios [C++], widen
ms.assetid: 4fdcd8e1-62d2-4611-8a70-1e4f58434007
ms.openlocfilehash: c22e048d01665deed83a9474525f414dfd874fe0
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62400651"
---
# <a name="basicios-class"></a>basic_ios 类

此模板类描述了依赖于模板参数的输入流（属于模板类 [basic_istream](../standard-library/basic-istream-class.md)）和输出流（属于模板类 [basic_ostream](../standard-library/basic-ostream-class.md)）通用的存储和成员函数。 （[ios_base](../standard-library/ios-base-class.md) 类描述不依赖于模板参数的通用内容。）类的对象**basic_ios\<class Elem，class >** 可帮助控制具有类型的元素的流`Elem`，其字符特征由类`Traits`。

## <a name="syntax"></a>语法

```cpp

template <class Elem, class Traits>
class basic_ios : public ios_base
```

### <a name="parameters"></a>参数

*Elem*<br/>
一种类型。

*特征*<br/>
`char_traits` 类型的变量。

## <a name="remarks"></a>备注

**basic_ios\<class Elem, class Traits>** 类的对象存储：

- 指向 [basic_istream](../standard-library/basic-istream-class.md)**\<Elem, Traits>** 类型的对象的绑定指针。

- 指向 [basic_streambuf](../standard-library/basic-streambuf-class.md)**\<Elem, Traits >** 类型的对象的流缓冲区指针。

- [格式设置信息](../standard-library/ios-base-class.md)。

- [ios_base](../standard-library/ios-base-class.md) 类型的基对象中的[流状态信息](../standard-library/ios-base-class.md)。

- `char_type` 类型的对象中的填充字符。

### <a name="constructors"></a>构造函数

|构造函数|描述|
|-|-|
|[basic_ios](#basic_ios)|构造 `basic_ios` 类。|

### <a name="typedefs"></a>Typedef

|类型名称|描述|
|-|-|
|[char_type](#char_type)|模板参数 `Elem` 的同义词。|
|[int_type](#int_type)|`Traits::int_type` 的同义词。|
|[off_type](#off_type)|`Traits::off_type` 的同义词。|
|[pos_type](#pos_type)|`Traits::pos_type` 的同义词。|
|[traits_type](#traits_type)|模板参数 `Traits` 的同义词。|

### <a name="member-functions"></a>成员函数

|成员函数|描述|
|-|-|
|[bad](#bad)|指示流缓冲区的完整性损失。|
|[clear](#clear)|清除所有错误标志。|
|[copyfmt](#copyfmt)|将标志从一个流复制到另一个流。|
|[eof](#eof)|指示是否已到达流的结尾。|
|[exceptions](#exceptions)|指示流将引发哪些异常。|
|[fail](#fail)|指示从流中提取有效字段失败。|
|[fill](#fill)|指定或返回在文本宽度小于流宽度时将使用的字符。|
|[good](#good)|指示流处于良好状态。|
|[imbue](#imbue)|更改区域设置。|
|[init](#init)|通过 `basic_ios` 构造函数调用。|
|[move](#move)|将所有值（指向流缓冲区的指针除外）从参数移动到当前对象。|
|[narrow](#narrow)|查找给定 `char_type` 的等效字符型。|
|[rdbuf](#rdbuf)|将流路由到指定缓冲区。|
|[rdstate](#rdstate)|读取标志的位状态。|
|[set_rdbuf](#set_rdbuf)|分配流缓冲区作为此流对象的读取缓冲区。|
|[setstate](#setstate)|设置其他标志。|
|[swap](#swap)|将此 `basic_ios` 对象中的值与另一个 `basic_ios` 对象中的值进行交换。 不会交换指向流缓冲区的指针。|
|[tie](#tie)|确保依次处理流。|
|[widen](#widen)|查找给定字符型的等效 `char_type`。|

### <a name="operators"></a>运算符

|运算符|描述|
|-|-|
|[explicit operator bool](#op_bool)|可以利用`basic_ios`对象作为**bool**。 禁用自动类型转换以防止产生常见的意外副作用。|
|[operator void *](#op_void_star)|指示流是否仍处于良好状态。|
|[operator!](#op_not)|指示流是否完好无损。|

## <a name="requirements"></a>要求

**标头：**\<ios>

**命名空间：** std

## <a name="bad"></a>  basic_ios::bad

指示流缓冲区的完整性损失

```cpp
bool bad() const;
```

### <a name="return-value"></a>返回值

**true**如果`rdstate & badbit`非零值; 否则为**false**。

有关 `badbit` 的详细信息，请参阅 [ios_base::iostate](../standard-library/ios-base-class.md#iostate)。

### <a name="example"></a>示例

```cpp
// basic_ios_bad.cpp
// compile with: /EHsc
#include <iostream>

int main( void )
{
    using namespace std;
    bool b = cout.bad( );
    cout << boolalpha;
    cout << b << endl;

    b = cout.good( );
    cout << b << endl;
}
```

## <a name="basic_ios"></a>  basic_ios::basic_ios

构造 basic_ios 类。

```cpp
explicit basic_ios(basic_streambuf<Elem,  Traits>* sb);
basic_ios();
```

### <a name="parameters"></a>参数

*sb*<br/>
用于存储输入或输出元素的标准缓冲区。

### <a name="remarks"></a>备注

第一个构造函数通过调用 [init](#init)(_ *Sb*) 可初始化其成员对象。 第二个（受保护的）构造函数取消初始化其成员对象。 更高版本调用`init`必须初始化对象，然后才可以安全地销毁。

## <a name="char_type"></a>  basic_ios::char_type

模板参数 `Elem` 的同义词。

```cpp
typedef Elem char_type;
```

## <a name="clear"></a>  basic_ios::clear

清除所有错误标志。

```cpp
void clear(iostate state = goodbit, bool reraise = false);
void clear(io_state state);
```

### <a name="parameters"></a>参数

*state*<br/>
（可选）你想要清除所有标志后设置标志。 默认为 `goodbit`。

*reraise*<br/>
（可选）指定是否应重新引发异常。 默认情况下**false** （不会重新引发异常）。

### <a name="remarks"></a>备注

标志为`goodbit`， `failbit`， `eofbit`，和`badbit`。 使用 [good](#good)、[bad](#bad)、[eof](#eof) 和 [fail](#fail) 测试这些标志

成员函数将存储的流状态信息替换为：

`state` &#124; `(`[rdbuf](#rdbuf) != 0 **goodbit** : **badbit**)

如果 `state`**&**[exceptions](#exceptions) 为非零，则它会抛出类 [failure](../standard-library/ios-base-class.md#failure) 的一个对象。

### <a name="example"></a>示例

请参阅[rdstate](#rdstate)并[getline](../standard-library/string-functions.md#getline)有关使用示例`clear`。

## <a name="copyfmt"></a>  basic_ios::copyfmt

将标志从一个流复制到另一个流。

```cpp
basic_ios<Elem, Traits>& copyfmt(
const basic_ios<Elem, Traits>& right);
```

### <a name="parameters"></a>参数

*right*<br/>
要复制其标志的流。

### <a name="return-value"></a>返回值

正在向其复制标志的流的 **this** 对象。

### <a name="remarks"></a>备注

成员函数将报告回调事件**擦除\_事件**。 然后将从复制*右* 成 **\*这** 填充字符、 绑定指针和格式设置信息。 之前更改异常掩码，它会报告回调事件`copyfmt_event`。 复制完成后，如果 **state &**[exceptions](#exceptions) 为非零，则该函数将有效地调用带参数 [rdstate](#rdstate) 的 [clear](#clear)。 它将返回 **\*this**。

### <a name="example"></a>示例

```cpp
// basic_ios_copyfmt.cpp
// compile with: /EHsc
#include <iostream>
#include <fstream>

int main( )
{
    using namespace std;
    ofstream x( "test.txt" );
    int i = 10;

    x << showpos;
    cout << i << endl;
    cout.copyfmt( x );
    cout << i << endl;
}
```

## <a name="eof"></a>  basic_ios::eof

指示是否已到达流的结尾。

```cpp
bool eof() const;
```

### <a name="return-value"></a>返回值

**true**如果已到达流结尾， **false**否则为。

### <a name="remarks"></a>备注

此成员函数返回 **，则返回 true**如果[rdstate](#rdstate) `& eofbit`为非零值。 有关 `eofbit` 的详细信息，请参阅 [ios_base::iostate](../standard-library/ios-base-class.md#iostate)。

### <a name="example"></a>示例

```cpp
// basic_ios_eof.cpp
// compile with: /EHsc
#include <iostream>
#include <fstream>

using namespace std;

int main( int argc, char* argv[] )
{
    fstream   fs;
    int n = 1;
    fs.open( "basic_ios_eof.txt" );   // an empty file
    cout << boolalpha
    cout << fs.eof() << endl;
    fs >> n;   // Read the char in the file
    cout << fs.eof() << endl;
}
```

## <a name="exceptions"></a>  basic_ios::exceptions

指示流将引发哪些异常。

```cpp
iostate exceptions() const;
void exceptions(iostate Newexcept);
void exceptions(io_state Newexcept);
```

### <a name="parameters"></a>参数

*Newexcept*<br/>
希望抛出异常的标志。

### <a name="return-value"></a>返回值

当前指定的用于为流抛出异常的标志。

### <a name="remarks"></a>备注

第一个成员函数返回存储的异常掩码。 第二个成员函数在异常掩码中存储 *_Except* 并返回其先前的存储值。 注意，存储新异常掩码会与调用 [clear](#clear)( [rdstate](#rdstate) ) 一样抛出异常。

### <a name="example"></a>示例

```cpp
// basic_ios_exceptions.cpp
// compile with: /EHsc /GR
#include <iostream>

int main( )
{
    using namespace std;

    cout << cout.exceptions( ) << endl;
    cout.exceptions( ios::eofbit );
    cout << cout.exceptions( ) << endl;
    try
    {
        cout.clear( ios::eofbit );   // Force eofbit on
    }
    catch ( exception &e )
    {
        cout.clear( );
        cout << "Caught the exception." << endl;
        cout << "Exception class: " << typeid(e).name()  << endl;
        cout << "Exception description: " << e.what() << endl;
    }
}
```

```Output
0
1
Caught the exception.
Exception class: class std::ios_base::failure
Exception description: ios_base::eofbit set
```

## <a name="fail"></a>  basic_ios::fail

指示从流中提取有效字段失败。

```cpp
bool fail() const;
```

### <a name="return-value"></a>返回值

**true**如果[rdstate](#rdstate) `& (badbit|failbit)`为零，否则**false**。

有关 `failbit` 的详细信息，请参阅 [ios_base::iostate](../standard-library/ios-base-class.md#iostate)。

### <a name="example"></a>示例

```cpp
// basic_ios_fail.cpp
// compile with: /EHsc
#include <iostream>

int main( void )
{
    using namespace std;
    bool b = cout.fail( );
    cout << boolalpha;
    cout << b << endl;
}
```

## <a name="fill"></a>  basic_ios::fill

指定或返回在文本宽度小于流宽度时将使用的字符。

```cpp
char_type fill() const;
char_type fill(char_type Char);
```

### <a name="parameters"></a>参数

*Char*<br/>
希望用作填充字符的字符。

### <a name="return-value"></a>返回值

当前的填充字符。

### <a name="remarks"></a>备注

第一个成员函数返回存储的填充字符。 第二个成员函数存储*Char*在填充字符并返回其先前的存储值。

### <a name="example"></a>示例

```cpp
// basic_ios_fill.cpp
// compile with: /EHsc
#include <iostream>
#include <iomanip>

int main( )
{
    using namespace std;

    cout << setw( 5 ) << 'a' << endl;
    cout.fill( 'x' );
    cout << setw( 5 ) << 'a' << endl;
    cout << cout.fill( ) << endl;
}
```

```Output
a
xxxxa
x
```

## <a name="good"></a>  basic_ios::good

指示流处于良好状态。

```cpp
bool good() const;
```

### <a name="return-value"></a>返回值

**true**如果[rdstate](#rdstate) `== goodbit` （未设置任何状态标志），否则为**false**。

有关 `goodbit` 的详细信息，请参阅 [ios_base::iostate](../standard-library/ios-base-class.md#iostate)。

### <a name="example"></a>示例

请参阅 [basic_ios:: bad](#bad)，了解使用 `good` 的示例。

## <a name="imbue"></a>  basic_ios::imbue

更改区域设置。

```cpp
locale imbue(const locale& Loc);
```

### <a name="parameters"></a>参数

*Loc*<br/>
区域设置字符串。

### <a name="return-value"></a>返回值

先前的区域设置。

### <a name="remarks"></a>备注

如果 [rdbuf](#rdbuf) 不是空指针，则成员函数将调用

`rdbuf`-> [pubimbue](../standard-library/basic-streambuf-class.md#pubimbue)(_ *Loc*)

不管怎样，它都将返回 [ios_base::imbue](../standard-library/ios-base-class.md#imbue)(_ *Loc*)。

### <a name="example"></a>示例

```cpp
// basic_ios_imbue.cpp
// compile with: /EHsc
#include <iostream>
#include <locale>

int main( )
{
    using namespace std;

    cout.imbue( locale( "french_france" ) );
    double x = 1234567.123456;
    cout << x << endl;
}
```

## <a name="init"></a>  basic_ios::init

由 basic_ios 构造函数调用。

```cpp
void init(basic_streambuf<Elem,Traits>* _Sb, bool _Isstd = false);
```

### <a name="parameters"></a>参数

*_Sb*<br/>
用于存储输入或输出元素的标准缓冲区。

*_Isstd*<br/>
指定这是否是一个标准流。

### <a name="remarks"></a>备注

成员函数将值存储在所有成员对象中，因此：

- [rdbuf](#rdbuf) 返回 *_Sb*。

- [tie](#tie) 返回空指针。

- [rdstate](#rdstate)将返回[goodbit](../standard-library/ios-base-class.md#iostate)如果 *_Sb*为非零值; 否则为它将返回[badbit](../standard-library/ios-base-class.md#iostate)。

- [异常](#exceptions)返回`goodbit`。

- [flags](../standard-library/ios-base-class.md#flags) 返回 [skipws](../standard-library/ios-base-class.md#fmtflags) &#124; [dec](../standard-library/ios-base-class.md#fmtflags)。

- [width](../standard-library/ios-base-class.md#width) 返回 0。

- [precision](../standard-library/ios-base-class.md#precision) 返回 6。

- [fill](#fill) 返回空格字符。

- [getloc](../standard-library/ios-base-class.md#getloc) 返回 `locale::classic`。

- [iword](../standard-library/ios-base-class.md#iword) 返回零，[pword](../standard-library/ios-base-class.md#pword) 返回针对所有参数值的空指针。

## <a name="int_type"></a>  basic_ios::int_type

`traits_type::int_type` 的同义词。

```cpp
typedef typename traits_type::int_type int_type;
```

## <a name="move"></a>  basic_ios::move

将所有值（指向流缓冲区的指针除外）从参数移动到当前对象。

```cpp
void move(basic_ios&& right);
```

### <a name="parameters"></a>参数

*right*<br/>
从中移动值的 `ios_base` 对象。

### <a name="remarks"></a>备注

受保护的成员函数将存储在中的所有值都移动*右*到`*this`除外存储`stream buffer pointer`，这不变的中*右*并将设置为 null 指针`*this`。 存储`tie pointer`设置为中的 null 指针*右*。

## <a name="narrow"></a>  basic_ios::narrow

查找给定 `char_type` 的等效字符型。

```cpp
char narrow(char_type Char, char Default = '\0') const;
```

### <a name="parameters"></a>参数

*Char*<br/>
**Char**转换。

*默认*<br/>
**Char**想要返回如果找到没有等效项。

### <a name="return-value"></a>返回值

等效于**char**到给定`char_type`。

### <a name="remarks"></a>备注

此成员函数返回[use_facet](../standard-library/basic-filebuf-class.md#open)\<ctype\<E >> ( [getloc](../standard-library/ios-base-class.md#getloc)（)）。`narrow`( `Char`, `Default`).

### <a name="example"></a>示例

```cpp
// basic_ios_narrow.cpp
// compile with: /EHsc
#include <ios>
#include <iostream>
#include <wchar.h>

int main( )
{
    using namespace std;
    wchar_t *x = L"test";
    char y[10];
    cout << x[0] << endl;
    wcout << x << endl;
    y[0] = wcout.narrow( x[0] );
    cout << y[0] << endl;
}
```

## <a name="off_type"></a>  basic_ios::off_type

`traits_type::off_type` 的同义词。

```cpp
typedef typename traits_type::off_type off_type;
```

## <a name="op_void_star"></a>  basic_ios::operator void *

指示流是否仍处于良好状态。

```cpp
operator void *() const;
```

### <a name="return-value"></a>返回值

仅在 [fail](#fail) 时，该运算符才会返回空指针。

### <a name="example"></a>示例

```cpp
// basic_ios_opgood.cpp
// compile with: /EHsc
#include <iostream>

int main( )
{
    using namespace std;
    cout << (bool)(&cout != 0) << endl;   // Stream is still good
}
```

```Output
1
```

## <a name="op_not"></a>  basic_ios::operator!

指示流是否完好无损。

```cpp
bool operator!() const;
```

### <a name="return-value"></a>返回值

返回 [fail](#fail)。

### <a name="example"></a>示例

```cpp
// basic_ios_opbad.cpp
// compile with: /EHsc
#include <iostream>

int main( )
{
    using namespace std;
    cout << !cout << endl;   // Stream is not bad
}
```

```Output
0
```

## <a name="op_bool"></a>  basic_ios::operator bool

可以利用`basic_ios`对象作为**bool**。 禁用自动类型转换以防止产生常见的意外副作用。

```cpp
explicit operator bool() const;
```

### <a name="remarks"></a>备注

该运算符将返回一个值可转换为**false**仅当`fail()`。 返回类型是转换仅为**bool**不为`void *`或其他已知的标量类型。

## <a name="pos_type"></a>  basic_ios::pos_type

`traits_type::pos_type` 的同义词。

```cpp
typedef typename traits_type::pos_type pos_type;
```

## <a name="rdbuf"></a>  basic_ios::rdbuf

将流路由到指定缓冲区。

```cpp
basic_streambuf<Elem, Traits> *rdbuf() const;
basic_streambuf<Elem, Traits> *rdbuf(
basic_streambuf<Elem, Traits>* _Sb);
```

### <a name="parameters"></a>参数

*_Sb*<br/>
一个流。

### <a name="remarks"></a>备注

第一个成员函数将返回存储的流缓冲区指针。

第二个成员函数存储 *_Sb*中存储的流缓冲区指针，并返回以前存储的值。

### <a name="example"></a>示例

```cpp
// basic_ios_rdbuf.cpp
// compile with: /EHsc
#include <ios>
#include <iostream>
#include <fstream>

int main( )
{
    using namespace std;
    ofstream file( "rdbuf.txt" );
    streambuf *x = cout.rdbuf( file.rdbuf( ) );
    cout << "test" << endl;   // Goes to file
    cout.rdbuf(x);
    cout << "test2" << endl;
}
```

```Output
test2
```

## <a name="rdstate"></a>  basic_ios::rdstate

读取标志的位状态。

```cpp
iostate rdstate() const;
```

### <a name="return-value"></a>返回值

存储的流状态信息。

### <a name="example"></a>示例

```cpp
// basic_ios_rdstate.cpp
// compile with: /EHsc
#include <iostream>
#include <fstream>
using namespace std;

void TestFlags( ios& x )
{
    cout << ( x.rdstate( ) & ios::badbit ) << endl;
    cout << ( x.rdstate( ) & ios::failbit ) << endl;
    cout << ( x.rdstate( ) & ios::eofbit ) << endl;
    cout << endl;
}

int main( )
{
    fstream x( "c:\test.txt", ios::out );
    x.clear( );
    TestFlags( x );
    x.clear( ios::badbit | ios::failbit | ios::eofbit );
    TestFlags( x );
}
```

```Output
0
0
0

4
2
1
```

## <a name="setstate"></a>  basic_ios::setstate

设置其他标志。

```cpp
void setstate(iostate _State);
```

### <a name="parameters"></a>参数

*_State*<br/>
要设置的其他标志。

### <a name="remarks"></a>备注

成员函数有效地调用 [clear](#clear)(_ *State* &#124; [rdstate](#rdstate))。

### <a name="example"></a>示例

```cpp
// basic_ios_setstate.cpp
// compile with: /EHsc
#include <ios>
#include <iostream>
using namespace std;

int main( )
{
    bool b = cout.bad( );
    cout << b << endl;   // Good
    cout.clear( ios::badbit );
    b = cout.bad( );
    // cout.clear( );
    cout << b << endl;   // Is bad, good
    b = cout.fail( );
    cout << b << endl;   // Not failed
    cout.setstate( ios::failbit );
    b = cout.fail( );
    cout.clear( );
    cout << b << endl;   // Is failed, good
    return 0;
}
```

```Output
0
1
```

## <a name="set_rdbuf"></a>  basic_ios::set_rdbuf

分配流缓冲区作为此流对象的读取缓冲区。

```cpp
void set_rdbuf(
basic_streambuf<Elem, Tr>* strbuf)
```

### <a name="parameters"></a>参数

*strbuf*<br/>
要成为读取缓冲区的流缓冲区。

### <a name="remarks"></a>备注

受保护的成员函数存储*strbuf*中`stream buffer pointer`。它不会调用`clear`。

## <a name="tie"></a>  basic_ios::tie

确保依次处理流。

```cpp
basic_ostream<Elem, Traits> *tie() const;
basic_ostream<Elem, Traits> *tie(
basic_ostream<Elem, Traits>* str);
```

### <a name="parameters"></a>参数

*str*<br/>
一个流。

### <a name="return-value"></a>返回值

第一个成员函数返回存储的绑定指针。 第二个成员函数存储*str*在绑定指针并返回其先前的存储值。

### <a name="remarks"></a>备注

`tie` 导致两个流同步，使得一个流上的操作在另一个流上的操作完成之后发生。

### <a name="example"></a>示例

在此例中，通过将 cin 绑定到 cout，可保证“输入数字:”字符串在该数字本身从 cin 提取之前进入控制台。 这消除了当读取相应数字时，“输入数字:”字符串仍在缓冲区中的可能性，使得我们确定用户实际上会得到一些提示来进行响应。 默认情况下，cin 和 cout 绑定在一起。

```cpp
#include <ios>
#include <iostream>

int main( )
{
    using namespace std;
    int i;
    cin.tie( &cout );
    cout << "Enter a number:";
    cin >> i;
}
```

## <a name="traits_type"></a>  basic_ios::traits_type

模板参数 `Traits` 的同义词。

```cpp
typedef Traits traits_type;
```

## <a name="widen"></a>  basic_ios::widen

查找等效`char_type`到给定**char**。

```cpp
char_type widen(char Char) const;
```

### <a name="parameters"></a>参数

*Char*<br/>
要转换的字符。

### <a name="return-value"></a>返回值

查找等效`char_type`到给定**char**。

### <a name="remarks"></a>备注

成员函数返回 [use_facet](../standard-library/basic-filebuf-class.md#open)< **ctype**\< **E**> >( [getloc](../standard-library/ios-base-class.md#getloc)). `widen`( `Char`).

### <a name="example"></a>示例

```cpp
// basic_ios_widen.cpp
// compile with: /EHsc
#include <ios>
#include <iostream>
#include <wchar.h>

int main( )
{
    using namespace std;
    char *z = "Hello";
    wchar_t y[2] = {0,0};
    cout << z[0] << endl;
    y[0] = wcout.widen( z[0] );
    wcout << &y[0] << endl;
}
```

## <a name="swap"></a>  basic_ios::swap

将此 `basic_ios` 对象中的值与另一个 `basic_ios` 对象中的值进行交换。 但是，不会交换指向流缓冲区的指针。

```cpp
void swap(basic_ios&& right);
```

### <a name="parameters"></a>参数

*right*<br/>
用于交换值的 `basic_ios` 对象。

### <a name="remarks"></a>备注

受保护的成员函数交换存储中的所有值*右*与`*this`除外存储`stream buffer pointer`。

## <a name="see-also"></a>请参阅

[C++ 标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)<br/>
[iostream 编程](../standard-library/iostream-programming.md)<br/>
[iostreams 约定](../standard-library/iostreams-conventions.md)<br/>
