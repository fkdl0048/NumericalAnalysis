# Numerical Analysis

## Numerical analysis and backround

definitions of computer number systems

floating point representation

representation of numbers in different bases

round-off errors.


### 십진수를 IEEE-754 부동소수점 표현

> Floating Point Representation

**EX)**

Convert 45.45 Decimal to 32-bit single precision IEEE-754 floating point representation.

> 45.45 십진수를 32비트 싱글 프리시전 IEEE-754 부동소수점 표현으로 변환하라.

부호부 (Sign) : 1비트. 숫자의 부호를 나타내며, 양수일 때 0, 음수일 때1이 됩니다.

지수부 (Exponent) :8비트. 지수를 나타냅니다.

가수부 (Mantissa) : 23비트. 가수 또는 유효숫자를 나타냅니다.

1. 부호부

가장 먼저 부호를 파악한다.  

45.45는 양수이므로 부호부는 0이 된다.

0|--------|-----------------------|

2. 가수부

두번째로 숫자의 절대값을 2진수로 표현한다.

$$ 45 = 22 * 2 + 1 $$
$$ 22 = 11 * 2 + 0 $$
$$ 11 = 5 * 2 + 1 $$
$$ 5 = 2 * 2 + 1 $$
$$ 2 = 1 * 2 + 0 $$
$$ 1 = 0 * 2 + 1 $$

나누기를 하여 나머지를 아래서부터 가져온다.

*비트로 계산하면 더 간단함 1 2 4 8 16 32 64 128 ..*

숫자를 조합하여 원하는 숫자를 만든다. 2의 제곱

따라서 정수부는 101101이 된다.

$$ 45 = 101101_{(2)} $$

소수부의 2진수 변환법

소수부에 2을 곱하면서 정수부는 버린다.

작성된 정수부를 위에서부터 가져온다.

$$ 0.45 * 2 = 0.9 $$
$$ 0.9 * 2 = 1.8 $$
$$ 0.8 * 2 = 1.6 $$
$$ 0.6 * 2 = 1.2 $$
$$ 0.2 * 2 = 0.4 $$
$$ 0.4 * 2 = 0.8 $$
$$ 0.8 * 2 = 1.6 $$
$$ 0.6 * 2 = 1.2 $$
$$ 0.2 * 2 = 0.4 $$
$$ 0.4 * 2 = 0.8 $$

반복..

$$ 0.45_{(10)} = 0.011100110110011001100..._{(2)} $$

자세히 보면 0.4부터는 반복적으로 무한하게 증식되기 때문에 0011의 형태로 반복된다.

따라서 소수부는 011100110110011001100...이 된다.

#### case 1

45.45의 경우 0.45가 무한하게 늘어날때 IEEE-754표현법에서는 23비트까지만 표현할 수 있다.  

하지만 45.45는 현재 

> 101101.0111001100110011001100110011001100110011001101

형태로 만들어지기 때문에 앞에서 부터 총 24자리까지만 생각을 하고 진행한다.

#### case 2

딱 나누어 떨어지는 경우는 남은 자리를 0으로 채운다.

---

다시 가수부로 돌아가서 구해진 숫자의 2진수 표현식에서 소수점을 왼쪽으로 옮겨서 오른쪽 1만 남게 만든다..

$$ 101101.01110011001100110011001100 $$
$$ 1.0110101110011001100110011001100 $$

그렇다면 다음과 같이 표현이 가능하다.

$$ 1.0110101110011001100110011001100 * 2^{5} $$

이를 **정규화된 표현 방식**이라고 한다.

구해진 소수부부분을 가수부 23비트의 앞에서 부터 채워 넣는다.

*남은 부분은 0으로 채운다.*

0|--------|01101011100110011001100|

3. 지수부

현재 지수는 5이다.

지수 5에 bias인 127을 더해준다.

$$ 5 + 127 $$
$$ 132 $$

이를 2진수로 변환한다.

$$ 132 = 66 * 2 + 0 $$
$$ 66 = 33 * 2 + 0 $$
$$ 33 = 16 * 2 + 1 $$
$$ 16 = 8 * 2 + 0 $$
$$ 8 = 4 * 2 + 0 $$
$$ 4 = 2 * 2 + 0 $$
$$ 2 = 1 * 2 + 0 $$
$$ 1 = 0 * 2 + 1 $$

$$ 132 = 10000100_{(2)} $$

이를 지수부에 채워 넣는다.

즉, 45.45를 32비트 단정도 부동소수점 방식으로 표현하면 다음과 같다.

0|10000100|01101011100110011001100|

0|10000100|01101011100110011001101|

..?

**EX)**

Convert 263.3 Decimal to 32-bit single precision IEEE-754 floating point representation.

> 263.3 소수점으로 32 비트 단일 정밀 IEEE-754 플로팅 포인트 표현을 변환하십시오.

1. 부호부

> 0|--------|-----------------------|

2. 가수부

$$ 263 = 131 * 2 + 1 $$
$$ 131 = 65 * 2 + 1 $$
$$ 65 = 32 * 2 + 1 $$
$$ 32 = 16 * 2 + 0 $$
$$ 16 = 8 * 2 + 0 $$
$$ 8 = 4 * 2 + 0 $$
$$ 4 = 2 * 2 + 0 $$
$$ 2 = 1 * 2 + 0 $$
$$ 1 = 0 * 2 + 1 $$

$$ 263 = 100000111{(2)} $$

$$ 0.3 * 2 = 0.6 $$
$$ 0.6 * 2 = 1.2 $$
$$ 0.2 * 2 = 0.4 $$
$$ 0.4 * 2 = 0.8 $$
$$ 0.8 * 2 = 1.6 $$
$$ 0.6 * 2 = 1.2 $$
$$ 0.2 * 2 = 0.4 $$
$$ 0.4 * 2 = 0.8 $$
$$ 0.8 * 2 = 1.6 $$
$$ 0.6 * 2 = 1.2 $$
$$ ... $$

$$ 0.3_{(10)} = 0.010011001100110011...{(2)} $$

$$ 263.3 = 100000111.010011001100110011... $$

$$ 1.000001110100110011001100110011... * 2^{8} $$

> 0|--------|00000111010011001100110|

3. 지수부

$$ 8 + 127 $$
$$ 135 $$

$$ 135 = 67 * 2 + 1 $$
$$ 67 = 33 * 2 + 1 $$
$$ 33 = 16 * 2 + 1 $$
$$ 16 = 8 * 2 + 0 $$
$$ 8 = 4 * 2 + 0 $$
$$ 4 = 2 * 2 + 0 $$
$$ 2 = 1 * 2 + 0 $$
$$ 1 = 0 * 2 + 1 $$

$$ 135 = 10000111_{(2)} $$

> 0|10000111|00000111010011001100110|

### 2진수를 10진수, 8진수, 2진수로 변환

Ex) 10101

#### 2진수를 10진수로 변환

위에서 다룬 기본적인 2의 제곱을 생각하면 된다.

1. 2진수의 각 자리수를 2의 제곱으로 변환한다.
2. 각 자리수를 곱한 값을 모두 더한다.

(간단..)

$$ 10101_{(2)} = 21_{(10)} $$

$$ 1 * 2^{4} + 0 * 2^{3} + 1 * 2^{2} + 0 * 2^{1} + 1 * 2^{0} $$
$$ 1 * 16 + 0 * 8 + 1 * 4 + 0 * 2 + 1 * 1 $$
$$ 16 + 4 + 1 $$
$$ 21 $$

#### 2진수를 8진수로 변환

8진수의 성격을 조금만 생각해보면 쉽게 답이 나온다.

앞서 2의 제곱수를 생각해서 1 2 4 8 16 32 64 128 256 512 ... 

이런식의 증가는 익숙하다.

그렇다면 8진수의 성격은 1 2 3 4 5 6 7 이후에 다시 10으로 시작하는 것이다.

즉, 8진수의 자리수가 8이 되면 1이 증가한다.

그럼 4bit를 생각해보면 `2^3 = 8`이니 4개씩 쪼개면 되나..? 라고 생각할 수 있지만 2진수를 계산하는 방법을 다시 보면 `1 + 2 + 4 = 7`이기 때문에 해당 자리수로 계산되면 4bit부터는 다음 자리수인걸 알 수 있다.

$$ 10101_{(2)} = 25_{(8)} $$
$$ 10|101 = 2|5 $$
$$ (2^{1} * 1 + 2^{0} * 0)| (2^2 * 1 + 2^1 * 0 + 2^0 * 1) = 2|5 $$
$$ (2 + 0) | (4 + 0 + 1) = 25 $$

#### 2진수를 16진수로 변환

8진수와 같은 맥락으로 1 + 2 + 4 + 8 = 15이기 때문에 4bit씩 쪼개면 된다.

$$ 10101_{(2)} = 15_{(16)} $$
$$ 1|0101 = 1|5 $$
$$ (2^{0} * 1) | (2^3 * 0 + 2^2 * 1 + 2^1 * 0 + 2^0 * 1) = 1|5 $$
$$ (1) | (0 + 4 + 0 + 1) = 15 $$

### 10진수를 2진수, 8진수, 16진수로 변환

$$ 117_{(10)} $$

#### 10진수를 2진수로 변환

IEEE-754표현법에서 사용했던 대로 10진수를 2진수로 변환하는 방법을 생각해보자.

1. 10진수를 2로 나눈다.
2. 나머지를 2진수로 변환한다.
3. 몫을 2로 나눈다.
4. 나머지를 2진수로 변환한다.
5. 몫을 2로 나눈다.
6. 나머지를 2진수로 변환한다.
7. ...

$$ 117 = 58 * 2 + 1 $$
$$ 58 = 29 * 2 + 0 $$
$$ 29 = 14 * 2 + 1 $$
$$ 14 = 7 * 2 + 0 $$
$$ 7 = 3 * 2 + 1 $$
$$ 3 = 1 * 2 + 1 $$
$$ 1 = 0 * 2 + 1 $$

$$ 117_{(10)} = 1110101_{(2)} $$

이렇게 정석적인 방법도 있지만 사실 쉬운 방법은 2의 제곱수를 생각하는 것이다.

$$ 2^{7} = 128 $$
$$ 2^{6} = 64 $$
$$ 2^{5} = 32 $$
$$ 2^{4} = 16 $$
$$ 2^{3} = 8 $$
$$ 2^{2} = 4 $$
$$ 2^{1} = 2 $$
$$ 2^{0} = 1 $$

$$ 117 = 64 + 32 + 16 + 4 + 1 $$

$$ 117_{(10)} = 1110101_{(2)} $$

#### 10진수를 8진수로 변환

위에서 사용한 같은 방법으로 2가아닌 8로 나누면 된다.

$$ 117 = 14 * 8 + 5 $$
$$ 14 = 1 * 8 + 6 $$
$$ 1 = 0 * 8 + 1 $$
$$ 117_{(10)} = 165_{(8)} $$

#### 10진수를 16진수로 변환

위에서 사용한 같은 방법으로 2가아닌 16로 나누면 된다.

$$ 117 = 7 * 16 + 5 $$
$$ 7 = 0 * 16 + 7 $$
$$ 117_{(10)} = 75_{(16)} $$

### 8진수를 2진수, 10진수, 16진수로 변환

$$ 345_{(8)} $$

#### 8진수를 2진수로 변환

8진수를 2진수로 변환하는 방법은 2진수를 8진수로 변환하는 방법과 같다.

각 자리수를 2진수로 변환하면 된다.

$$ 3|4|5 = (011)|(100)|(101)$$
$$ 345_{(8)} = 011100101_{(2)} $$

#### 8진수를 10진수로 변환

각 자리수에 8의 제곱수를 곱한 후 더하면 된다.

$$ 345_{(8)} = (3 * 8^2) + (4 * 8^1) + (5 * 8^0) $$

$$ 345_{(8)} = 229_{(10)} $$

#### 8진수를 16진수로 변환

8진수를 16진수로 변환하는 방법은 우선 8진수를 2진수로 변환한 후 2진수를 16진수로 변환하면 된다.

위에서 8진수를 2진수로 변환한 결과를 사용한다.

$$ 3|4|5 = (011)|(100)|(101)$$
$$ 345_{(8)} = 011100101_{(2)} $$

이제 여기서 변환된 2진수를 16진수로 변환하면 된다.

2진수의 특성은 3bit씩 잘라서 보면 8진수 4bit씩 잘라서 보면 16진수이다.

$$ 1110|0101 = E5_{(16)} $$
$$ 345_{(8)} = E5_{(16)} $$

### 16진수를 2진수, 8진수, 10진수로 변환

$$ AE5{(16)} $$

#### 16진수를 2진수로 변환

분해는 조립의 역순이다.

$$ AE5{(16)} = 1010|1110|0101 $$
$$ AE5{(16)} = 101011100101_{(2)} $$

#### 16진수를 8진수로 변환

16진수를 8진수로 변환하는 방법은 16진수를 2진수로 변환한 후 2진수를 8진수로 변환하면 된다.

위에서 16진수를 2진수로 변환한 결과를 사용한다.

$$ AE5{(16)} = 101011100101_{(2)} $$
$$ AE5{(16)} = 101|011|100|101 $$
$$ AE5{(16)} = 5345_{(8)} $$

#### 16진수를 10진수로 변환

16진수를 10진수로 변환하는 방법은 각 자리수에 16의 제곱수를 곱한 후 더하면 된다.

$$ AE5{(16)} = (10 * 16^2) + (14 * 16^1) + (5 * 16^0) $$
$$ 2560 + 224 + 5 = 2789 $$
$$ AE5{(16)} = 2789_{(10)} $$


### 소수점 이하 유효숫자 자리 반올림

> 13.947536

2, 3, 5자리수 반올림하기..!

2의 자리

$$ 13.947536 = 13.95 $$

3의 자리

$$ 13.947536 = 13.948 $$

5의 자리

$$ 13.947536 = 13.94754 $$

## Root Finding

### Bisection method

$$ 𝑥^2 − 2 = 0 $$

*three decimal places.*

$$ F(0) = (0)^2 - 2 = -2 $$

$$ F(1) = (1)^2 - 2 = -1 $$

$$ F(2) = (2)^2 - 2 = 2 $$

$$ a = 1, b = 2 $$

$$ x_1 = \frac{a+b}{2} = \frac{1+2}{2} = 1.5 $$

$$ F(1.5) = (1.5)^2 - 2 = 0.25 $$

$$ 0.25 > 0 $$

$$ x_2 = \frac{a+b}{2} = \frac{1+1.5}{2} = 1.25 $$

$$ F(1.25) = (1.25)^2 - 2 = -0.4375 $$

$$ -0.4375 < 0 $$

$$ x_3 = \frac{a+b}{2} = \frac{1.25+1.5}{2} = 1.375 $$

$$ F(1.375) = (1.375)^2 - 2 = -0.109375 $$

$$ -0.109375 < 0 $$

$$ x_4 = \frac{a+b}{2} = \frac{1.375+1.5}{2} = 1.4375 $$

$$ F(1.4375) = (1.4375)^2 - 2 = 0.06640625 $$

$$ 0.06640625 > 0 $$

$$ x_5 = \frac{a+b}{2} = \frac{1.375 + 1.4375}{2} = 1.40625 $$

$$ F(1.40625) = (1.40625)^2 - 2 = -0.0224609375 $$

$$ -0.0224609375 < 0 $$

$$ x_6 = \frac{a+b}{2} = \frac{1.40625 + 1.4375}{2} = 1.421875 $$

$$ F(1.421875) = (1.421875)^2 - 2 = 0.021728515625 $$

$$ 0.021728515625 > 0 $$

$$ x_7 = \frac{a+b}{2} = \frac{1.40625 + 1.421875}{2} = 1.4140625 $$

$$ F(1.4140625) = (1.4140625)^2 - 2 = -0.00042724609375 $$

$$ -0.00042724609375 < 0 $$

$$ x_8 = \frac{a+b}{2} = \frac{1.4140625 + 1.421875}{2} = 1.41796875 $$

$$ F(1.41796875) = (1.41796875)^2 - 2 = 0.0106353759765625 $$

$$ 0.0106353759765625 > 0 $$

$$ x_9 = \frac{a+b}{2} = \frac{1.4140625 + 1.41796875}{2} = 1.416015625 $$

$$ F(1.416015625) = (1.416015625)^2 - 2 = 0.0051002502441406 $$

$$ 0.0051002502441406 > 0 $$

$$ x_{10} = \frac{a+b}{2} = \frac{1.4140625 + 1.416015625}{2} = 1.4150390625 $$

$$ F(1.4150390625) = (1.4150390625)^2 - 2 = 0.0023355484008789 $$

$$ 0.0023355484008789 > 0 $$

$$ x_{11} = \frac{a+b}{2} = \frac{1.4140625 + 1.4150390625}{2} = 1.41455078125 $$

$$ F(1.41455078125) = (1.41455078125)^2 - 2 = 0.0009539127349853515625 $$

$$ 0.0009539127349853515625 > 0 $$

$$ x_{12} = \frac{a+b}{2} = \frac{1.4140625 + 1.41455078125}{2} = 1.414306640625 $$

$$ F(1.414306640625) = (1.414306640625)^2 - 2 = 0.000263273715972900390625 $$

$$ 0.000263273715972900390625 > 0 $$

$$ x_{13} = \frac{a+b}{2} = \frac{1.4140625 + 1.414306640625}{2} = 1.4141845703125 $$

$$ 1.4141..... $$

### fixed-point iteration

$$ x^3- 7x + 3 $$

using **fixed point iteration method**, correct upto 3-decimal places.

### Newton's method 

$$ 𝑥^3 − 48 $$


using **newton-Raphson method**, correct upto 4-decimal places. 

### False Position Method

### Secant Method

## Direct Methods for Solving Linear Systems

### Gaussian elimination

### LU decomposition

## Quiz

퀴즈 내용 및 족보 내용 적기