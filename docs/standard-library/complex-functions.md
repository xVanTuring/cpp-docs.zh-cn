---
title: '&lt;complex&gt; 函数'
ms.date: 11/04/2016
f1_keywords:
- xcomplex/std::abs
- xcomplex/std::acos
- xcomplex/std::acosh
- xcomplex/std::arg
- xcomplex/std::conj
- xcomplex/std::cos
- xcomplex/std::cosh
- xcomplex/std::exp
- xxcomplex/std::imag
- xcomplex/std::log
- xcomplex/std::log10
- xcomplex/std::norm
- xcomplex/std::polar
- xcomplex/std::pow
- xxcomplex/std::real
- xcomplex/std::sin
- xcomplex/std::sinh
- xcomplex/std::sqrt
- xcomplex/std::tan
- xcomplex/std::tanh
ms.assetid: 58b14e94-0e0c-493e-8237-8b4d685904a2
helpviewer_keywords:
- std::abs [C++]
- std::arg [C++]
- std::conj [C++]
- std::cos [C++]
- std::cosh [C++]
- std::exp [C++]
- std::imag [C++]
- std::log [C++]
- std::log10
- std::norm [C++]
- std::polar [C++]
- std::pow [C++]
- std::real [C++]
- std::sin [C++]
- std::sinh [C++]
- std::sqrt [C++]
- std::tan [C++]
- std::tanh [C++]
ms.openlocfilehash: a67955da21c1229c3492d5b52dd6e14c9caa33fd
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62389198"
---
# <a name="ltcomplexgt-functions"></a>&lt;complex&gt; 函数

||||
|-|-|-|
|[abs](#abs)|[arg](#arg)|[conj](#conj)|
|[cos](#cos)|[cosh](#cosh)|[exp](#exp)|
|[imag](#imag)|[log](#log)|[log10](#log10)|
|[norm](#norm)|[polar](#polar)|[pow](#pow)|
|[real](#real)|[sin](#sin)|[sinh](#sinh)|
|[sqrt](#sqrt)|[tan](#tan)|[tanh](#tanh)|

## <a name="abs"></a>  abs

计算复数的模数。

```cpp
template <class Type>
Type abs(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要确定取模的复数。

### <a name="return-value"></a>返回值

复数取模。

### <a name="remarks"></a>备注

复数的*取模*是测量表示复数矢量的长度。 复数取模                         a + bi 为                         sqrt (a<sup>2</sup> + b<sup>2</sup>)，写作                        &#124；a + bi&#124；。 复数的 *norm*                          a + bi 为 (a<sup>2</sup> + b<sup>2</sup>)，因此复数的取模是其 norm 的平方根。

### <a name="example"></a>示例

```cpp
// complex_abs.cpp
// compile with: /EHsc
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   double pi = 3.14159265359;

   // Complex numbers can be entered in polar form with
   // modulus and argument parameter inputs but are
   // stored in Cartesian form as real & imag coordinates
   complex <double> c1 ( polar ( 5.0 ) );   // Default argument = 0
   complex <double> c2 ( polar ( 5.0 , pi / 6 ) );
   complex <double> c3 ( polar ( 5.0 , 13 * pi / 6 ) );
   cout << "c1 = polar ( 5.0 ) = " << c1 << endl;
   cout << "c2 = polar ( 5.0 , pi / 6 ) = " << c2 << endl;
   cout << "c3 = polar ( 5.0 , 13 * pi / 6 ) = " << c3 << endl;

   // The modulus and argument of a complex number can be recovered
   // using abs & arg member functions
   double absc1 = abs ( c1 );
   double argc1 = arg ( c1 );
   cout << "The modulus of c1 is recovered from c1 using: abs ( c1 ) = "
        << absc1 << endl;
   cout << "Argument of c1 is recovered from c1 using:\n arg ( c1 ) = "
        << argc1 << " radians, which is " << argc1 * 180 / pi
        << " degrees." << endl;

   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is recovered from c2 using: abs ( c2 ) = "
        << absc2 << endl;
   cout << "Argument of c2 is recovered from c2 using:\n arg ( c2 ) = "
        << argc2 << " radians, which is " << argc2 * 180 / pi
        << " degrees." << endl;

   // Testing if the principal angles of c2 and c3 are the same
   if ( (arg ( c2 ) <= ( arg ( c3 ) + .00000001) ) ||
        (arg ( c2 ) >= ( arg ( c3 ) - .00000001) ) )
      cout << "The complex numbers c2 & c3 have the "
           << "same principal arguments."<< endl;
   else
      cout << "The complex numbers c2 & c3 don't have the "
           << "same principal arguments." << endl;
}
```

```Output
c1 = polar ( 5.0 ) = (5,0)
c2 = polar ( 5.0 , pi / 6 ) = (4.33013,2.5)
c3 = polar ( 5.0 , 13 * pi / 6 ) = (4.33013,2.5)
The modulus of c1 is recovered from c1 using: abs ( c1 ) = 5
Argument of c1 is recovered from c1 using:
arg ( c1 ) = 0 radians, which is 0 degrees.
The modulus of c2 is recovered from c2 using: abs ( c2 ) = 5
Argument of c2 is recovered from c2 using:
arg ( c2 ) = 0.523599 radians, which is 30 degrees.
The complex numbers c2 & c3 have the same principal arguments.
```

## <a name="arg"></a>  arg

从复数中提取自变量。

```cpp
template <class Type>
Type arg(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要确定参数的复数。

### <a name="return-value"></a>返回值

复数的参数。

### <a name="remarks"></a>备注

*自变量*是复杂矢量发出复平面中的正实轴的角度。 对于复数*a + bi*，参数等于反正切值 (*b / a*)。 该角度从正实轴以逆时针方向测量时为正值，以顺时针方向测量时则为负值。 主体的值是大于-pi 且小于于或等于 + pi。

### <a name="example"></a>示例

```cpp
// complex_arg.cpp
// compile with: /EHsc
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   double pi = 3.14159265359;

   // Complex numbers can be entered in polar form with
   // modulus and argument parameter inputs but are
   // stored in Cartesian form as real & imag coordinates
   complex <double> c1 ( polar ( 5.0 ) );   // Default argument = 0
   complex <double> c2 ( polar ( 5.0 , pi / 6 ) );
   complex <double> c3 ( polar ( 5.0 , 13 * pi / 6 ) );
   cout << "c1 = polar ( 5.0 ) = " << c1 << endl;
   cout << "c2 = polar ( 5.0 , pi / 6 ) = " << c2 << endl;
   cout << "c3 = polar ( 5.0 , 13 * pi / 6 ) = " << c3 << endl;

   // The modulus and argument of a complex number can be rcovered
   // using abs & arg member functions
   double absc1 = abs ( c1 );
   double argc1 = arg ( c1 );
   cout << "The modulus of c1 is recovered from c1 using: abs ( c1 ) = "
        << absc1 << endl;
   cout << "Argument of c1 is recovered from c1 using:\n arg ( c1 ) = "
        << argc1 << " radians, which is " << argc1 * 180 / pi
        << " degrees." << endl;

   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is recovered from c2 using: abs ( c2 ) = "
        << absc2 << endl;
   cout << "Argument of c2 is recovered from c2 using:\n arg ( c2 ) = "
        << argc2 << " radians, which is " << argc2 * 180 / pi
        << " degrees." << endl;

   // Testing if the principal angles of c2 and c3 are the same
   if ( (arg ( c2 ) <= ( arg ( c3 ) + .00000001) ) ||
        (arg ( c2 ) >= ( arg ( c3 ) - .00000001) ) )
      cout << "The complex numbers c2 & c3 have the "
           << "same principal arguments."<< endl;
   else
      cout << "The complex numbers c2 & c3 don't have the "
           << "same principal arguments." << endl;
}
```

```Output
c1 = polar ( 5.0 ) = (5,0)
c2 = polar ( 5.0 , pi / 6 ) = (4.33013,2.5)
c3 = polar ( 5.0 , 13 * pi / 6 ) = (4.33013,2.5)
The modulus of c1 is recovered from c1 using: abs ( c1 ) = 5
Argument of c1 is recovered from c1 using:
arg ( c1 ) = 0 radians, which is 0 degrees.
The modulus of c2 is recovered from c2 using: abs ( c2 ) = 5
Argument of c2 is recovered from c2 using:
arg ( c2 ) = 0.523599 radians, which is 30 degrees.
The complex numbers c2 & c3 have the same principal arguments.
```

## <a name="conj"></a>  conj

返回复数的复数共轭。

```cpp
template <class Type>
complex<Type> conj(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要返回的复共轭的复数。

### <a name="return-value"></a>返回值

输入复数的复共轭。

### <a name="remarks"></a>备注

复数的复数共轭*a + bi*是*a-bi*。 复数及其共轭的乘积是数 *a*2 + *b*2 的 norm。

### <a name="example"></a>示例

```cpp
// complex_conj.cpp
// compile with: /EHsc
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;

   complex <double> c1 ( 4.0 , 3.0 );
   cout << "The complex number c1 = " << c1 << endl;

   double dr1 = real ( c1 );
   cout << "The real part of c1 is real ( c1 ) = "
        << dr1 << "." << endl;

   double di1 = imag ( c1 );
   cout << "The imaginary part of c1 is imag ( c1 ) = "
        << di1 << "." << endl;

   complex <double> c2 = conj ( c1 );
   cout << "The complex conjugate of c1 is c2 = conj ( c1 )= "
        << c2 << endl;

   double dr2 = real ( c2 );
   cout << "The real part of c2 is real ( c2 ) = "
        << dr2 << "." << endl;

   double di2 = imag ( c2 );
   cout << "The imaginary part of c2 is imag ( c2 ) = "
        << di2 << "." << endl;

   // The real part of the product of a complex number
   // and its conjugate is the norm of the number
   complex <double> c3 = c1 * c2;
   cout << "The norm of (c1 * conj (c1) ) is c1 * c2 = "
        << real( c3 ) << endl;
}
```

```Output
The complex number c1 = (4,3)
The real part of c1 is real ( c1 ) = 4.
The imaginary part of c1 is imag ( c1 ) = 3.
The complex conjugate of c1 is c2 = conj ( c1 )= (4,-3)
The real part of c2 is real ( c2 ) = 4.
The imaginary part of c2 is imag ( c2 ) = -3.
The norm of (c1 * conj (c1) ) is c1 * c2 = 25
```

## <a name="cos"></a>  cos

返回复数的余弦值。

```cpp
template <class Type>
complex<Type> cos(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要确定其余弦的复数。

### <a name="return-value"></a>返回值

输入复数的余弦的复数。

### <a name="remarks"></a>备注

定义复余弦的标识：

cos ( *z*) = (1/2)\*( exp ( *iz*) + exp (- *iz*) )

cos ( *z*) = cos ( *a* + *bi*) = cos ( *a*) cosh ( *b*) - isin ( *a*) sinh ( *b*)

### <a name="example"></a>示例

```cpp
// complex_cos.cpp
// compile with: /EHsc
#include <vector>
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   double pi = 3.14159265359;
   complex <double> c1 ( 3.0 , 4.0 );
   cout << "Complex number c1 = " << c1 << endl;

   // Values of cosine of a complex number c1
   complex <double> c2 = cos ( c1 );
   cout << "Complex number c2 = cos ( c1 ) = " << c2 << endl;
   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is: " << absc2 << endl;
   cout << "The argument of c2 is: "<< argc2 << " radians, which is "
        << argc2 * 180 / pi << " degrees." << endl << endl;

   // Cosines of the standard angles in the first
   // two quadrants of the complex plane
   vector <complex <double> > v1;
   vector <complex <double> >::iterator Iter1;
   complex <double> vc1  ( polar (1.0, pi / 6) );
   v1.push_back( cos ( vc1 ) );
   complex <double> vc2  ( polar (1.0, pi / 3) );
   v1.push_back( cos ( vc2 ) );
   complex <double> vc3  ( polar (1.0, pi / 2) );
   v1.push_back( cos ( vc3) );
   complex <double> vc4  ( polar (1.0, 2 * pi / 3) );
   v1.push_back( cos ( vc4 ) );
   complex <double> vc5  ( polar (1.0, 5 * pi / 6) );
   v1.push_back( cos ( vc5 ) );
   complex <double> vc6  ( polar (1.0,  pi ) );
   v1.push_back( cos ( vc6 ) );

   cout << "The complex components cos (vci), where abs (vci) = 1"
        << "\n& arg (vci) = i * pi / 6 of the vector v1 are:\n" ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << endl;
}
```

```Output
Complex number c1 = (3,4)
Complex number c2 = cos ( c1 ) = (-27.0349,-3.85115)
The modulus of c2 is: 27.3079
The argument of c2 is: -3.00009 radians, which is -171.893 degrees.

The complex components cos (vci), where abs (vci) = 1
& arg (vci) = i * pi / 6 of the vector v1 are:
(0.730543,-0.39695)
(1.22777,-0.469075)
(1.54308,1.21529e-013)
(1.22777,0.469075)
(0.730543,0.39695)
(0.540302,-1.74036e-013)
```

## <a name="cosh"></a>  cosh

返回复数的双曲余弦值。

```cpp
template <class Type>
complex<Type> cosh(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要确定其双曲余弦的复数。

### <a name="return-value"></a>返回值

输入复数的双曲余弦的复数。

### <a name="remarks"></a>备注

定义复双曲余弦的标识：

cos ( *z*) = (1/2)\*( exp ( *z*) + exp (- *z*) )

cos ( *z*) = cosh ( *a + bi*) = cosh ( *a*) cos ( *b*) + isinh ( *a*) sin ( *b*)

### <a name="example"></a>示例

```cpp
// complex_cosh.cpp
// compile with: /EHsc
#include <vector>
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   double pi = 3.14159265359;
   complex <double> c1 ( 3.0 , 4.0 );
   cout << "Complex number c1 = " << c1 << endl;

   // Values of cosine of a complex number c1
   complex <double> c2 = cosh ( c1 );
   cout << "Complex number c2 = cosh ( c1 ) = " << c2 << endl;
   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is: " << absc2 << endl;
   cout << "The argument of c2 is: "<< argc2 << " radians, which is "
        << argc2 * 180 / pi << " degrees." << endl << endl;

   // Hyperbolic cosines of the standard angles
   // in the first two quadrants of the complex plane
   vector <complex <double> > v1;
   vector <complex <double> >::iterator Iter1;
   complex <double> vc1  ( polar (1.0, pi / 6) );
   v1.push_back( cosh ( vc1 ) );
   complex <double> vc2  ( polar (1.0, pi / 3) );
   v1.push_back( cosh ( vc2 ) );
   complex <double> vc3  ( polar (1.0, pi / 2) );
   v1.push_back( cosh ( vc3) );
   complex <double> vc4  ( polar (1.0, 2 * pi / 3) );
   v1.push_back( cosh ( vc4 ) );
   complex <double> vc5  ( polar (1.0, 5 * pi / 6) );
   v1.push_back( cosh ( vc5 ) );
   complex <double> vc6  ( polar (1.0,  pi ) );
   v1.push_back( cosh ( vc6 ) );

   cout << "The complex components cosh (vci), where abs (vci) = 1"
        << "\n& arg (vci) = i * pi / 6 of the vector v1 are:\n" ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << endl;
}
```

```Output
Complex number c1 = (3,4)
Complex number c2 = cosh ( c1 ) = (-6.58066,-7.58155)
The modulus of c2 is: 10.0392
The argument of c2 is: -2.28564 radians, which is -130.957 degrees.

The complex components cosh (vci), where abs (vci) = 1
& arg (vci) = i * pi / 6 of the vector v1 are:
(1.22777,0.469075)
(0.730543,0.39695)
(0.540302,-8.70178e-014)
(0.730543,-0.39695)
(1.22777,-0.469075)
(1.54308,2.43059e-013)
```

## <a name="exp"></a>  exp

返回复数的指数函数。

```cpp
template <class Type>
complex<Type> exp(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要确定其指数的复数。

### <a name="return-value"></a>返回值

输入复数的指数的复数。

### <a name="example"></a>示例

```cpp
// complex_exp.cpp
// compile with: /EHsc
#include <vector>
#include <complex>
#include <iostream>

int main() {
   using namespace std;
   double pi = 3.14159265359;
   complex <double> c1 ( 1 , pi/6 );
   cout << "Complex number c1 = " << c1 << endl;

   // Value of exponential of a complex number c1:
   // note the argument of c2 is determined by the
   // imaginary part of c1 & the modulus by the real part
   complex <double> c2 = exp ( c1 );
   cout << "Complex number c2 = exp ( c1 ) = " << c2 << endl;
   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is: " << absc2 << endl;
   cout << "The argument of c2 is: "<< argc2 << " radians, which is "
        << argc2 * 180 / pi << " degrees." << endl << endl;

   // Exponentials of the standard angles
   // in the first two quadrants of the complex plane
   vector <complex <double> > v1;
   vector <complex <double> >::iterator Iter1;
   complex <double> vc1  ( 0.0 , -pi );
   v1.push_back( exp ( vc1 ) );
   complex <double> vc2  ( 0.0, -2 * pi / 3 );
   v1.push_back( exp ( vc2 ) );
   complex <double> vc3  ( 0.0, 0.0 );
   v1.push_back( exp ( vc3 ) );
   complex <double> vc4  ( 0.0, pi / 3 );
   v1.push_back( exp ( vc4 ) );
   complex <double> vc5  ( 0.0 , 2 * pi / 3 );
   v1.push_back( exp ( vc5 ) );
   complex <double> vc6  ( 0.0, pi );
   v1.push_back( exp ( vc6 ) );

   cout << "The complex components exp (vci), where abs (vci) = 1"
        << "\n& arg (vci) = i * pi / 3 of the vector v1 are:\n" ;
   for ( Iter1 = v1.begin() ; Iter1 != v1.end() ; Iter1++ )
      cout <<  ( * Iter1 ) << "\n     with argument = "
           << ( 180/pi ) * arg ( *Iter1 )
           << " degrees\n     modulus = "
           << abs ( * Iter1 ) << endl;
}
```

## <a name="imag"></a>  imag

提取复数的虚分量。

```cpp
template <class Type>
Type imag(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要提取其实部的复数。

### <a name="return-value"></a>返回值

作为全局函数的复数的虚部。

### <a name="remarks"></a>备注

此模板函数无法用于修改复数的实部。 要更改实部，必须为新复数分配分量值。

### <a name="example"></a>示例

```cpp
// complexc_imag.cpp
// compile with: /EHsc
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   complex <double> c1 ( 4.0 , 3.0 );
   cout << "The complex number c1 = " << c1 << endl;

   double dr1 = real ( c1 );
   cout << "The real part of c1 is real ( c1 ) = "
        << dr1 << "." << endl;

   double di1 = imag ( c1 );
   cout << "The imaginary part of c1 is imag ( c1 ) = "
        << di1 << "." << endl;
}
```

```Output
The complex number c1 = (4,3)
The real part of c1 is real ( c1 ) = 4.
The imaginary part of c1 is imag ( c1 ) = 3.
```

## <a name="log"></a>  log

返回复数的自然对数。

```cpp
template <class Type>
complex<Type> log(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要确定其自然对数的复数。

### <a name="return-value"></a>返回值

输入复数的自然对数的复数。

### <a name="remarks"></a>备注

沿负实轴的分支剪切。

### <a name="example"></a>示例

```cpp
// complex_log.cpp
// compile with: /EHsc
#include <vector>
#include <complex>
#include <iostream>

int main() {
   using namespace std;
   double pi = 3.14159265359;
   complex <double> c1 ( 3.0 , 4.0 );
   cout << "Complex number c1 = " << c1 << endl;

   // Values of log of a complex number c1
   complex <double> c2 = log ( c1 );
   cout << "Complex number c2 = log ( c1 ) = " << c2 << endl;
   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is: " << absc2 << endl;
   cout << "The argument of c2 is: "<< argc2 << " radians, which is "
        << argc2 * 180 / pi << " degrees." << endl << endl;

   // log of the standard angles
   // in the first two quadrants of the complex plane
   vector <complex <double> > v1;
   vector <complex <double> >::iterator Iter1;
   complex <double> vc1  ( polar (1.0, pi / 6) );
   v1.push_back( log ( vc1 ) );
   complex <double> vc2  ( polar (1.0, pi / 3) );
   v1.push_back( log ( vc2 ) );
   complex <double> vc3  ( polar (1.0, pi / 2) );
   v1.push_back( log ( vc3) );
   complex <double> vc4  ( polar (1.0, 2 * pi / 3) );
   v1.push_back( log ( vc4 ) );
   complex <double> vc5  ( polar (1.0, 5 * pi / 6) );
   v1.push_back( log ( vc5 ) );
   complex <double> vc6  ( polar (1.0,  pi ) );
   v1.push_back( log ( vc6 ) );

   cout << "The complex components log (vci), where abs (vci) = 1 "
        << "\n& arg (vci) = i * pi / 6 of the vector v1 are:\n" ;
   for ( Iter1 = v1.begin() ; Iter1 != v1.end() ; Iter1++ )
      cout << *Iter1 << " " << endl;
}
```

## <a name="log10"></a>  log10

返回复数的以 10 为底的对数。

```cpp
template <class Type>
complex<Type> log10(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要确定以 10 为底的对数的复数。

### <a name="return-value"></a>返回值

输入复数以 10 为底的对数的复数。

### <a name="remarks"></a>备注

沿负实轴的分支剪切。

### <a name="example"></a>示例

```cpp
// complex_log10.cpp
// compile with: /EHsc
#include <vector>
#include <complex>
#include <iostream>

int main() {
   using namespace std;
   double pi = 3.14159265359;
   complex <double> c1 ( 3.0 , 4.0 );
   cout << "Complex number c1 = " << c1 << endl;

   // Values of log10 of a complex number c1
   complex <double> c2 = log10 ( c1 );
   cout << "Complex number c2 = log10 ( c1 ) = " << c2 << endl;
   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is: " << absc2 << endl;
   cout << "The argument of c2 is: "<< argc2 << " radians, which is "
        << argc2 * 180 / pi << " degrees." << endl << endl;

   // log10 of the standard angles
   // in the first two quadrants of the complex plane
   vector <complex <double> > v1;
   vector <complex <double> >::iterator Iter1;
   complex <double> vc1  ( polar (1.0, pi / 6) );
   v1.push_back( log10 ( vc1 ) );
   complex <double> vc2  ( polar (1.0, pi / 3) );
   v1.push_back( log10 ( vc2 ) );
   complex <double> vc3  ( polar (1.0, pi / 2) );
   v1.push_back( log10 ( vc3) );
   complex <double> vc4  ( polar (1.0, 2 * pi / 3) );
   v1.push_back( log10 ( vc4 ) );
   complex <double> vc5  ( polar (1.0, 5 * pi / 6) );
   v1.push_back( log10 ( vc5 ) );
   complex <double> vc6  ( polar (1.0,  pi ) );
   v1.push_back( log10 ( vc6 ) );

   cout << "The complex components log10 (vci), where abs (vci) = 1"
        << "\n& arg (vci) = i * pi / 6 of the vector v1 are:\n" ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << endl;
}
```

## <a name="norm"></a>  norm

提取复数的范数。

```cpp
template <class Type>
Type norm(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要确定其 norm 的复数。

### <a name="return-value"></a>返回值

复数的 norm。

### <a name="remarks"></a>备注

复数 *a + bi* 的 norm 为 *(a*<sup>2</sup> *+ b*<sup>2</sup>*)。* 复数的 norm 是其取模的平方。 复数的取模是测量表示复数矢量的长度。 复数 *a + bi* 的取模为 `sqrt`*(a*<sup>2</sup> *+ b*<sup>2</sup>*)，* 写作 *&#124；a + bi&#124；。*

### <a name="example"></a>示例

```cpp
// complex_norm.cpp
// compile with: /EHsc
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   double pi = 3.14159265359;

   // Complex numbers can be entered in polar form with
   // modulus and argument parameter inputs but are
   // stored in Cartesian form as real & imag coordinates
   complex <double> c1 ( polar ( 5.0 ) );   // Default argument = 0
   complex <double> c2 ( polar ( 5.0 , pi / 6 ) );
   complex <double> c3 ( polar ( 5.0 , 13 * pi / 6 ) );
   cout << "c1 = polar ( 5.0 ) = " << c1 << endl;
   cout << "c2 = polar ( 5.0 , pi / 6 ) = " << c2 << endl;
   cout << "c3 = polar ( 5.0 , 13 * pi / 6 ) = " << c3 << endl;

   if ( (arg ( c2 ) <= ( arg ( c3 ) + .00000001) ) ||
        (arg ( c2 ) >= ( arg ( c3 ) - .00000001) ) )
      cout << "The complex numbers c2 & c3 have the "
           << "same principal arguments."<< endl;
   else
      cout << "The complex numbers c2 & c3 don't have the "
           << "same principal arguments." << endl;

   // The modulus and argument of a complex number can be recovered
   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is recovered from c2 using: abs ( c2 ) = "
        << absc2 << endl;
   cout << "Argument of c2 is recovered from c2 using:\n arg ( c2 ) = "
        << argc2 << " radians, which is " << argc2 * 180 / pi
        << " degrees." << endl;

   // The norm of a complex number is the square of its modulus
   double normc2 = norm ( c2 );
   double sqrtnormc2 = sqrt ( normc2 );
   cout << "The norm of c2 given by: norm ( c2 ) = " << normc2 << endl;
   cout << "The modulus of c2 is the square root of the norm: "
        << "sqrt ( normc2 ) = " << sqrtnormc2 << ".";
}
```

```Output
c1 = polar ( 5.0 ) = (5,0)
c2 = polar ( 5.0 , pi / 6 ) = (4.33013,2.5)
c3 = polar ( 5.0 , 13 * pi / 6 ) = (4.33013,2.5)
The complex numbers c2 & c3 have the same principal arguments.
The modulus of c2 is recovered from c2 using: abs ( c2 ) = 5
Argument of c2 is recovered from c2 using:
arg ( c2 ) = 0.523599 radians, which is 30 degrees.
The norm of c2 given by: norm ( c2 ) = 25
The modulus of c2 is the square root of the norm: sqrt ( normc2 ) = 5.
```

## <a name="polar"></a>  polar

返回以笛卡尔坐标形式表示的，对应于指定模数和自变量的复数。

```cpp
template <class Type>
complex<Type> polar(const Type& _Modulus, const Type& _Argument = 0);
```

### <a name="parameters"></a>参数

*_Modulus*<br/>
所输入的复数取模。

*_Argument*<br/>
所输入的复数的参数。

### <a name="return-value"></a>返回值

极坐标视图中指定的复数的笛卡尔视图。

### <a name="remarks"></a>备注

复数的极坐标图的形式提供了取模*r*和参数*p*，其中这些参数与实部和虚部笛卡尔组件和*b*通过公式 = r \* cos *p*并*b* = *r* \* sin *p*。

### <a name="example"></a>示例

```cpp
// complex_polar.cpp
// compile with: /EHsc
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   double pi = 3.14159265359;

   // Complex numbers can be entered in polar form with
   // modulus and argument parameter inputs but are
   // stored in Cartesian form as real & imag coordinates
   complex <double> c1 ( polar ( 5.0 ) );   // Default argument = 0
   complex <double> c2 ( polar ( 5.0 , pi / 6 ) );
   complex <double> c3 ( polar ( 5.0 , 13 * pi / 6 ) );
   cout << "c1 = polar ( 5.0 ) = " << c1 << endl;
   cout << "c2 = polar ( 5.0 , pi / 6 ) = " << c2 << endl;
   cout << "c3 = polar ( 5.0 , 13 * pi / 6 ) = " << c3 << endl;

   if ( (arg ( c2 ) <= ( arg ( c3 ) + .00000001) ) ||
        (arg ( c2 ) >= ( arg ( c3 ) - .00000001) ) )
      cout << "The complex numbers c2 & c3 have the "
           << "same principal arguments."<< endl;
   else
      cout << "The complex numbers c2 & c3 don't have the "
           << "same principal arguments." << endl;

   // the modulus and argument of a complex number can be rcovered
   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is recovered from c2 using: abs ( c2 ) = "
        << absc2 << endl;
   cout << "Argument of c2 is recovered from c2 using:\n arg ( c2 ) = "
        << argc2 << " radians, which is " << argc2 * 180 / pi
        << " degrees." << endl;
}
```

```Output
c1 = polar ( 5.0 ) = (5,0)
c2 = polar ( 5.0 , pi / 6 ) = (4.33013,2.5)
c3 = polar ( 5.0 , 13 * pi / 6 ) = (4.33013,2.5)
The complex numbers c2 & c3 have the same principal arguments.
The modulus of c2 is recovered from c2 using: abs ( c2 ) = 5
Argument of c2 is recovered from c2 using:
arg ( c2 ) = 0.523599 radians, which is 30 degrees.
```

## <a name="pow"></a>  pow

计算通过进行底数为复数的另一个复数次幂运算获得的复数。

```cpp
template <class Type>
complex<Type> pow(const complex<Type>& _Base, int _Power);

template <class Type>
complex<Type> pow(const complex<Type>& _Base, const Type& _Power);

template <class Type>
complex<Type> pow(const complex<Type>& _Base, const complex<Type>& _Power);

template <class Type>
complex<Type> pow(const Type& _Base, const complex<Type>& _Power);
```

### <a name="parameters"></a>参数

*_Base*<br/>
复数或属于复数参数类型的数是基数由成员函数升幂的基数。

*_Power*<br/>
整数或复数或属于复数参数类型的数是由成员函数升底数的幂。

### <a name="return-value"></a>返回值

通过提升指定幂的指定基数获取复数。

### <a name="remarks"></a>备注

这些函数各自有效地将这两个操作转换为返回类型，并将转换后的 **left** 返回到幂 **right**。

沿负实轴的分支剪切。

### <a name="example"></a>示例

```cpp
// complex_pow.cpp
// compile with: /EHsc
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   double pi = 3.14159265359;

   // First member function
   // type complex<double> base & type integer power
   complex <double> cb1 ( 3 , 4);
   int cp1 = 2;
   complex <double> ce1 = pow ( cb1 ,cp1 );

   cout << "Complex number for base cb1 = " << cb1 << endl;
   cout << "Integer for power = " << cp1 << endl;
   cout << "Complex number returned from complex base and integer power:"
        << "\n ce1 = cb1 ^ cp1 = " << ce1 << endl;
   double absce1 = abs ( ce1 );
   double argce1 = arg ( ce1 );
   cout << "The modulus of ce1 is: " << absce1 << endl;
   cout << "The argument of ce1 is: "<< argce1 << " radians, which is "
        << argce1 * 180 / pi << " degrees." << endl << endl;

   // Second member function
   // type complex<double> base & type double power
   complex <double> cb2 ( 3 , 4 );
   double cp2 = pi;
   complex <double> ce2 = pow ( cb2 ,cp2 );

   cout << "Complex number for base cb2 = " << cb2 << endl;
   cout << "Type double for power cp2 = pi = " << cp2 << endl;
   cout << "Complex number returned from complex base and double power:"
        << "\n ce2 = cb2 ^ cp2 = " << ce2 << endl;
   double absce2 = abs ( ce2 );
   double argce2 = arg ( ce2 );
   cout << "The modulus of ce2 is: " << absce2 << endl;
   cout << "The argument of ce2 is: "<< argce2 << " radians, which is "
        << argce2 * 180 / pi << " degrees." << endl << endl;

   // Third member function
   // type complex<double> base & type complex<double> power
   complex <double> cb3 ( 3 , 4 );
   complex <double> cp3 ( -2 , 1 );
   complex <double> ce3 = pow ( cb3 ,cp3 );

   cout << "Complex number for base cb3 = " << cb3 << endl;
   cout << "Complex number for power cp3= " << cp3 << endl;
   cout << "Complex number returned from complex base and complex power:"
        << "\n ce3 = cb3 ^ cp3 = " << ce3 << endl;
   double absce3 = abs ( ce3 );
   double argce3 = arg ( ce3 );
   cout << "The modulus of ce3 is: " << absce3 << endl;
   cout << "The argument of ce3 is: "<< argce3 << " radians, which is "
        << argce3 * 180 / pi << " degrees." << endl << endl;

   // Fourth member function
   // type double base & type complex<double> power
   double cb4 = pi;
   complex <double> cp4 ( 2 , -1 );
   complex <double> ce4 = pow ( cb4 ,cp4 );

   cout << "Type double for base cb4 = pi = " << cb4 << endl;
   cout << "Complex number for power cp4 = " << cp4 << endl;
   cout << "Complex number returned from double base and complex power:"
        << "\n ce4 = cb4 ^ cp4 = " << ce4 << endl;
   double absce4 = abs ( ce4 );
   double argce4 = arg ( ce4 );
   cout << "The modulus of ce4 is: " << absce4 << endl;
   cout << "The argument of ce4 is: "<< argce4 << " radians, which is "
        << argce4 * 180 / pi << " degrees." << endl << endl;
}
```

```Output
Complex number for base cb1 = (3,4)
Integer for power = 2
Complex number returned from complex base and integer power:
ce1 = cb1 ^ cp1 = (-7,24)
The modulus of ce1 is: 25
The argument of ce1 is: 1.85459 radians, which is 106.26 degrees.

Complex number for base cb2 = (3,4)
Type double for power cp2 = pi = 3.14159
Complex number returned from complex base and double power:
ce2 = cb2 ^ cp2 = (-152.915,35.5475)
The modulus of ce2 is: 156.993
The argument of ce2 is: 2.91318 radians, which is 166.913 degrees.

Complex number for base cb3 = (3,4)
Complex number for power cp3= (-2,1)
Complex number returned from complex base and complex power:
ce3 = cb3 ^ cp3 = (0.0153517,-0.00384077)
The modulus of ce3 is: 0.0158249
The argument of ce3 is: -0.245153 radians, which is -14.0462 degrees.

Type double for base cb4 = pi = 3.14159
Complex number for power cp4 = (2,-1)
Complex number returned from double base and complex power:
ce4 = cb4 ^ cp4 = (4.07903,-8.98725)
The modulus of ce4 is: 9.8696
The argument of ce4 is: -1.14473 radians, which is -65.5882 degrees.
```

## <a name="real"></a>  real

提取复数的实分量。

```cpp
template <class Type>
Type real(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要提取其实部的复数。

### <a name="return-value"></a>返回值

作为全局函数的复数的实部。

### <a name="remarks"></a>备注

此模板函数无法用于修改复数的实部。 要更改实部，必须为新复数分配分量值。

### <a name="example"></a>示例

```cpp
// complex_real.cpp
// compile with: /EHsc
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   complex <double> c1 ( 4.0 , 3.0 );
   cout << "The complex number c1 = " << c1 << endl;

   double dr1 = real ( c1 );
   cout << "The real part of c1 is real ( c1 ) = "
        << dr1 << "." << endl;

   double di1 = imag ( c1 );
   cout << "The imaginary part of c1 is imag ( c1 ) = "
        << di1 << "." << endl;
}
```

```Output
The complex number c1 = (4,3)
The real part of c1 is real ( c1 ) = 4.
The imaginary part of c1 is imag ( c1 ) = 3.
```

## <a name="sin"></a>  sin

返回复数的正弦值。

```cpp
template <class Type>
complex<Type> sin(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要确定其正弦的复数。

### <a name="return-value"></a>返回值

输入复数的正弦的复数。

### <a name="remarks"></a>备注

定义复正弦的标识：

sin ( *z*) = (1/2 *i*)\*( exp ( *iz*) - exp (- *iz*) )

sin ( *z*) = sin ( *a + bi*) = sin ( *a*) cosh ( *b*) + icos ( *a*) sinh ( *b*)

### <a name="example"></a>示例

```cpp
// complex_sin.cpp
// compile with: /EHsc
#include <vector>
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   double pi = 3.14159265359;
   complex <double> c1 ( 3.0 , 4.0 );
   cout << "Complex number c1 = " << c1 << endl;

   // Values of sine of a complex number c1
   complex <double> c2 = sin ( c1 );
   cout << "Complex number c2 = sin ( c1 ) = " << c2 << endl;
   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is: " << absc2 << endl;
   cout << "The argument of c2 is: "<< argc2 << " radians, which is "
        << argc2 * 180 / pi << " degrees." << endl << endl;

   // sines of the standard angles in the first
   // two quadrants of the complex plane
   vector <complex <double> > v1;
   vector <complex <double> >::iterator Iter1;
   complex <double> vc1  ( polar ( 1.0, pi / 6 ) );
   v1.push_back( sin ( vc1 ) );
   complex <double> vc2  ( polar ( 1.0, pi / 3 ) );
   v1.push_back( sin ( vc2 ) );
   complex <double> vc3  ( polar ( 1.0, pi / 2 ) );
   v1.push_back( sin ( vc3 ) );
   complex <double> vc4  ( polar ( 1.0, 2 * pi / 3 ) );
   v1.push_back( sin ( vc4 ) );
   complex <double> vc5  ( polar ( 1.0, 5 * pi / 6 ) );
   v1.push_back( sin ( vc5 ) );
   complex <double> vc6  ( polar ( 1.0, pi ) );
   v1.push_back( sin ( vc6 ) );

   cout << "The complex components sin (vci), where abs (vci) = 1"
        << "\n& arg (vci) = i * pi / 6 of the vector v1 are:\n" ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << endl;
}
```

```Output
Complex number c1 = (3,4)
Complex number c2 = sin ( c1 ) = (3.85374,-27.0168)
The modulus of c2 is: 27.2903
The argument of c2 is: -1.42911 radians, which is -81.882 degrees.

The complex components sin (vci), where abs (vci) = 1
& arg (vci) = i * pi / 6 of the vector v1 are:
(0.85898,0.337596)
(0.670731,0.858637)
(-1.59572e-013,1.1752)
(-0.670731,0.858637)
(-0.85898,0.337596)
(-0.841471,-1.11747e-013)
```

## <a name="sinh"></a>  sinh

返回复数的双曲正弦值。

```cpp
template <class Type>
complex<Type> sinh(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要确定其双曲正弦的复数。

### <a name="return-value"></a>返回值

输入复数的双曲正弦的复数。

### <a name="remarks"></a>备注

定义复双曲正弦的标识：

sinh ( *z*) = (1/2)\*( exp ( *z*) - exp (- *z*) )

sinh ( *z*) = sinh ( *a + bi*) = sinh ( *a*) cos ( *b*) + *i*cosh ( *a*) sin ( *b*)

### <a name="example"></a>示例

```cpp
// complex_sinh.cpp
// compile with: /EHsc
#include <vector>
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   double pi = 3.14159265359;
   complex <double> c1 ( 3.0 , 4.0 );
   cout << "Complex number c1 = " << c1 << endl;

   // Values of sine of a complex number c1
   complex <double> c2 = sinh ( c1 );
   cout << "Complex number c2 = sinh ( c1 ) = " << c2 << endl;
   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is: " << absc2 << endl;
   cout << "The argument of c2 is: "<< argc2 << " radians, which is "
        << argc2 * 180 / pi << " degrees." << endl << endl;

   // Hyperbolic sines of the standard angles in
   // the first two quadrants of the complex plane
   vector <complex <double> > v1;
   vector <complex <double> >::iterator Iter1;
   complex <double> vc1  ( polar ( 1.0, pi / 6 ) );
   v1.push_back( sinh ( vc1 ) );
   complex <double> vc2  ( polar ( 1.0, pi / 3 ) );
   v1.push_back( sinh ( vc2 ) );
   complex <double> vc3  ( polar ( 1.0, pi / 2 ) );
   v1.push_back( sinh ( vc3) );
   complex <double> vc4  ( polar ( 1.0, 2 * pi / 3 ) );
   v1.push_back( sinh ( vc4 ) );
   complex <double> vc5  ( polar ( 1.0, 5 * pi / 6 ) );
   v1.push_back( sinh ( vc5 ) );
   complex <double> vc6  ( polar ( 1.0, pi ) );
   v1.push_back( sinh ( vc6 ) );

   cout << "The complex components sinh (vci), where abs (vci) = 1"
        << "\n& arg (vci) = i * pi / 6 of the vector v1 are:\n" ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << endl;
}
```

```Output
Complex number c1 = (3,4)
Complex number c2 = sinh ( c1 ) = (-6.54812,-7.61923)
The modulus of c2 is: 10.0464
The argument of c2 is: -2.28073 radians, which is -130.676 degrees.

The complex components sinh (vci), where abs (vci) = 1
& arg (vci) = i * pi / 6 of the vector v1 are:
(0.858637,0.670731)
(0.337596,0.85898)
(-5.58735e-014,0.841471)
(-0.337596,0.85898)
(-0.858637,0.670731)
(-1.1752,-3.19145e-013)
```

## <a name="sqrt"></a>  sqrt

计算复数的平方根。

```cpp
template <class Type>
complex<Type> sqrt(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
将查找其平方根的复数。

### <a name="return-value"></a>返回值

复数的平方根。

### <a name="remarks"></a>备注

平方根将在半开放间隔中具有一个阶段角度 (-pi/2，pi/2]。

沿负实轴的复平面中的分支剪切。

复数的平方根将具有输入数的平方根的取模，以及输入数一半数的参数。

### <a name="example"></a>示例

```cpp
// complex_sqrt.cpp
// compile with: /EHsc
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   double pi = 3.14159265359;

   // Complex numbers can be entered in polar form with
   // modulus and argument parameter inputs but are
   // stored in Cartesian form as real & imag coordinates
   complex <double> c1 ( polar ( 25.0 , pi / 2 ) );
   complex <double> c2 = sqrt ( c1 );
   cout << "c1 = polar ( 5.0 ) = " << c1 << endl;
   cout << "c2 = sqrt ( c1 ) = " << c2 << endl;

   // The modulus and argument of a complex number can be recovered
   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is recovered from c2 using: abs ( c2 ) = "
        << absc2 << endl;
   cout << "Argument of c2 is recovered from c2 using:\n arg ( c2 ) = "
        << argc2 << " radians, which is " << argc2 * 180 / pi
        << " degrees." << endl;

   // The modulus and argument of c2 can be directly calculated
   absc2 = sqrt( abs ( c1 ) );
   argc2 = 0.5 * arg ( c1 );
   cout << "The modulus of c2 = sqrt( abs ( c1 ) ) =" << absc2 << endl;
   cout << "The argument of c2 = ( 1 / 2 ) * arg ( c1 ) ="
        << argc2 << " radians,\n which is " << argc2 * 180 / pi
        << " degrees." << endl;
}
```

```Output
c1 = polar ( 5.0 ) = (-2.58529e-012,25)
c2 = sqrt ( c1 ) = (3.53553,3.53553)
The modulus of c2 is recovered from c2 using: abs ( c2 ) = 5
Argument of c2 is recovered from c2 using:
arg ( c2 ) = 0.785398 radians, which is 45 degrees.
The modulus of c2 = sqrt( abs ( c1 ) ) =5
The argument of c2 = ( 1 / 2 ) * arg ( c1 ) =0.785398 radians,
which is 45 degrees.
```

## <a name="tan"></a> tan

返回复数的正切值。

```cpp
template <class Type>
complex<Type> tan(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要确定其正切的复数。

### <a name="return-value"></a>返回值

输入复数的正切的复数。

### <a name="remarks"></a>备注

定义复正切的标识：

tan ( *z*) = sin ( *z*) / cos ( *z*) = ( exp ( *iz*) - exp (- *iz*) ) / *i*( exp ( *iz*) + exp (- *iz*) )

### <a name="example"></a>示例

```cpp
// complex_tan.cpp
// compile with: /EHsc
#include <vector>
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   double pi = 3.14159265359;
   complex <double> c1 ( 3.0 , 4.0 );
   cout << "Complex number c1 = " << c1 << endl;

   // Values of cosine of a complex number c1
   complex <double> c2 = tan ( c1 );
   cout << "Complex number c2 = tan ( c1 ) = " << c2 << endl;
   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is: " << absc2 << endl;
   cout << "The argument of c2 is: "<< argc2 << " radians, which is "
        << argc2 * 180 / pi << " degrees." << endl << endl;

   // Hyperbolic tangent of the standard angles
   // in the first two quadrants of the complex plane
   vector <complex <double> > v1;
   vector <complex <double> >::iterator Iter1;
   complex <double> vc1  ( polar ( 1.0, pi / 6 ) );
   v1.push_back( tan ( vc1 ) );
   complex <double> vc2  ( polar ( 1.0, pi / 3 ) );
   v1.push_back( tan ( vc2 ) );
   complex <double> vc3  ( polar ( 1.0, pi / 2 ) );
   v1.push_back( tan ( vc3) );
   complex <double> vc4  ( polar ( 1.0, 2 * pi / 3 ) );
   v1.push_back( tan ( vc4 ) );
   complex <double> vc5  ( polar ( 1.0, 5 * pi / 6 ) );
   v1.push_back( tan ( vc5 ) );
   complex <double> vc6  ( polar ( 1.0,  pi ) );
   v1.push_back( tan ( vc6 ) );

   cout << "The complex components tan (vci), where abs (vci) = 1"
        << "\n& arg (vci) = i * pi / 6 of the vector v1 are:\n" ;
   for ( Iter1 = v1.begin() ; Iter1 != v1.end() ; Iter1++ )
      cout << *Iter1 << endl;
}
```

```Output
Complex number c1 = (3,4)
Complex number c2 = tan ( c1 ) = (-0.000187346,0.999356)
The modulus of c2 is: 0.999356
The argument of c2 is: 1.57098 radians, which is 90.0107 degrees.

The complex components tan (vci), where abs (vci) = 1
& arg (vci) = i * pi / 6 of the vector v1 are:
(0.713931,0.85004)
(0.24356,0.792403)
(-4.34302e-014,0.761594)
(-0.24356,0.792403)
(-0.713931,0.85004)
(-1.55741,-7.08476e-013)
```

## <a name="tanh"></a>  tanh

返回复数的双曲正切值。

```cpp
template <class Type>
complex<Type> tanh(const complex<Type>& complexNum);
```

### <a name="parameters"></a>参数

*complexNum*<br/>
要确定其双曲正切的复数。

### <a name="return-value"></a>返回值

输入复数的双曲正切的复数。

### <a name="remarks"></a>备注

定义复双曲余切的标识：

tanh ( *z*) = sinh ( *z*) / cosh ( *z*) = ( exp ( *z*) - exp (- *z*) ) / ( exp ( *z*) + exp (- *z*) )

### <a name="example"></a>示例

```cpp
// complex_tanh.cpp
// compile with: /EHsc
#include <vector>
#include <complex>
#include <iostream>

int main( )
{
   using namespace std;
   double pi = 3.14159265359;
   complex <double> c1 ( 3.0 , 4.0 );
   cout << "Complex number c1 = " << c1 << endl;

   // Values of cosine of a complex number c1
   complex <double> c2 = tanh ( c1 );
   cout << "Complex number c2 = tanh ( c1 ) = " << c2 << endl;
   double absc2 = abs ( c2 );
   double argc2 = arg ( c2 );
   cout << "The modulus of c2 is: " << absc2 << endl;
   cout << "The argument of c2 is: "<< argc2 << " radians, which is "
        << argc2 * 180 / pi << " degrees." << endl << endl;

   // Hyperbolic tangents of the standard angles
   // in the first two quadrants of the complex plane
   vector <complex <double> > v1;
   vector <complex <double> >::iterator Iter1;
   complex <double> vc1  ( polar ( 1.0, pi / 6 ) );
   v1.push_back( tanh ( vc1 ) );
   complex <double> vc2  ( polar ( 1.0, pi / 3 ) );
   v1.push_back( tanh ( vc2 ) );
   complex <double> vc3  ( polar ( 1.0, pi / 2 ) );
   v1.push_back( tanh ( vc3 ) );
   complex <double> vc4  ( polar ( 1.0, 2 * pi / 3 ) );
   v1.push_back( tanh ( vc4 ) );
   complex <double> vc5  ( polar ( 1.0, 5 * pi / 6 ) );
   v1.push_back( tanh ( vc5 ) );
   complex <double> vc6  ( polar ( 1.0, pi ) );
   v1.push_back( tanh ( vc6 ) );

   cout << "The complex components tanh (vci), where abs (vci) = 1"
        << "\n& arg (vci) = i * pi / 6 of the vector v1 are:\n" ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << endl;
}
```

```Output
Complex number c1 = (3,4)
Complex number c2 = tanh ( c1 ) = (1.00071,0.00490826)
The modulus of c2 is: 1.00072
The argument of c2 is: 0.00490474 radians, which is 0.281021 degrees.

The complex components tanh (vci), where abs (vci) = 1
& arg (vci) = i * pi / 6 of the vector v1 are:
(0.792403,0.24356)
(0.85004,0.713931)
(-3.54238e-013,1.55741)
(-0.85004,0.713931)
(-0.792403,0.24356)
(-0.761594,-8.68604e-014)
```

## <a name="see-also"></a>请参阅

[\<complex>](../standard-library/complex.md)<br/>
