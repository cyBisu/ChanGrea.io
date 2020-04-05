---
title: 'RegExp(정규식)'
date: 2019-09-28 23:09:07
category: javascript
---

## RegExp(정규표현식)이란?

- 정규 표현식은 문자열에 나타나는 특정 문자 조합과 대응시키기 위해 사용되는 패턴
- `RegExp`의 `exec`, `test` 메소드와 `String`의 `match`, `replace`, `search`, `split` 메소드와 함께 사용

실제 **RegExp를 만들어서 활용하는 과정**은 아래와 같다.

#### :one: [RegExp를 만든다.](#regexp-만드는-방법)

:point_right: RegExp [패턴](#1-특수-문자와-그-의미)과 [플래그](#2-플래그)를 참고해서 생성

#### :two: [RegExp와 String 메소드와 함께 사용](#정규식-사용하기)

## RegExp 만드는 방법

### 1. '/' 이용(정규식 리터럴을 사용하는 방법)

```javascript
var re = /ab+c/;
```

- `스크립트 로딩 시` 컴파일

### 2. RegExp 생성자 이용

```javascript
var re = new RegExp('ab+c');
```

- `실행 시점`에 컴파일

## 정규식 패턴 작성

정규식 패턴 작성하는 방법에는 두 가지가 있다고 한다. 그 중 하나는 **단순한 패턴으로 작성하는 방법**인데, 예를 들어서 '/abc/'라는 패턴은 단순히 abc가 들어가 있는 문자열을 찾는 것이다.

하지만, 우리가 RegExp를 사용하는 목적은 단순하게 저런 문자열 찾고자 하는게 아니지 않은가...?
그래서 지금부터는 **특수 문자를 사용하는 방법**에 대해서 보겠다.

### 1. 특수 문자와 그 의미

| Character | Meaning                                                                                                                                                      |
| :-------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \         | \ 뒤에 오는 문자는 무시한다. 즉 \ 뒤에 오는 문자는 **특수한 의미**(예를들어 모든 숫자를 뜻하는 `d`)나 **특수 문자**(예를 들어 `*`)를 일반 문자로 인식한다.   |
| ^         | ^ 뒤에 오는 문자로 시작하는 문자열                                                                                                                           |
| \$        | \$ 앞에 있는 문자로 끝나는 문자열                                                                                                                            |
| \*        | 앞에 있는 문자가 0회 이상 반복                                                                                                                               |
| +         | 앞에 있는 문자가 1회 이상 반복                                                                                                                               |
| ?         | 앞에 있는 문자가 0회 또는 1회                                                                                                                                |
| .         | 개행 문자를 제외한 모든 단일 문자                                                                                                                            |
| (x)       | 'x'와 일치하는 문자 또는 문자열                                                                                                                              |
| x(?=y)    | x 뒤에 y가 있는 경우                                                                                                                                         |
| x(?!y)    | x 뒤에 y가 없는 경우                                                                                                                                         |
| x\|y      | x 또는 y인 경우                                                                                                                                              |
| {n}       | 앞에 있는 표현식이 n( n은 숫자 )번 나오는 경우                                                                                                               |
| {n,m}     | 앞에 있는 표현식이 최소 n번, 최대 m번 나오는 경우                                                                                                            |
| [xyz]     | Character set, 괄호 안에 있는 문자 집합에 해당하는 경우<br />ex)<br />[a-d] :point_right: [abcd]와 같으며, "brisket"에서 b에 일치, "city"에서 c에 일치       |
| [\^xyz]   | Character set에 있는 문자를 제외                                                                                                                             |
| [\b]      | 백스페이스에 대응                                                                                                                                            |
| \b        | 단어의 경계를 뜻함<br />ex)<br />/\bm/ :point_right: "moon"에 m에 대응<br />/oo\b/ :point_right: "moon"에 oo에 **대응하지 않음** (뒤에 n이 나오기 때문이다.) |
| \d        | 숫자에 대응, [0-9]와 같다.                                                                                                                                   |
| \D        | 숫자가 아닌 것에 대응, [\^0-9]와 같다.                                                                                                                       |
| \n        | 줄 바꿈                                                                                                                                                      |
| \r        | Carrage Return                                                                                                                                               |
| \s        | Space, Tab, 줄 바꿈 등 공백문자<br />[`\f` `\n` `\r` `\t` `\v` `\u00a0` `\u1680` `\u2000` `\u200a` `\u2028` `\u2029` `\u202f` `\u205f` `\u3000` `\ufeff` ]   |
| \S        | 공백문자가 아닌 것들<br />[\^ `\f` `\n` `\r` `\t` `\v` `\u00a0` `\u1680` `\u2000` `\u200a` `\u2028` `\u2029` `\u202f` `\u205f` `\u3000` `\ufeff` ]           |
| \t        | Tab                                                                                                                                                          |
| \v        | 수직 Tab                                                                                                                                                     |
| \w        | 밑줄 문자를 포함한 영숫자 문자<br />[A-Za-z0-9_]                                                                                                             |
| \W        | 단어 문자가 아닌 문자<br />[\^A-Za-z0-9_]                                                                                                                    |
| \0        | null 문자                                                                                                                                                    |

여기까지가 정규식의 패턴을 작성하는 특수기호에 대한 내용이었다.

### 2. 플래그

> 한가지 더, 정규식 패턴 뒤에 `플래그`라는 것을 옵션으로 붙여줄 수 있다.

**플래그**는 아래와 같이 정규식 패턴 뒤에 붙여준다.

```javascript
var re = /pattern/flags;
//or
var re = new RegExp("pattern", "flags");
```

**플래그**의 종류는 아래에 있는 것들 정도만 참고하자.

| Flag  | Description               |
| ----- | ------------------------- |
| **g** | `전역` 검색               |
| **i** | `대소문자 구분 없는` 검색 |
| **m** | `다중행(multi-line)` 검색 |

## 정규식 사용하기

위에서 언급했듯이, 정규식은 **RegExp**의 `exec`, `test`, `match` 메소드와 **String**의 `search`, `replace`, `split` 메소드와 함께 쓰인다.

각각의 메소드에 대해서 설명하자면 아래와 같다.

| Method      | Description                                                                                                                                                                                                           |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **exec**    | 대응되는 문자열을 찾는 `RegExp` 메소드<br />정보를 가지고 있는 `array` return (찾지 못했다면 `null` return)                                                                                                           |
| **test**    | 대응되는 문자열이 있는지 검사하는 RegExp 메소드<br />`true`or `false` return                                                                                                                                          |
| **match**   | 대응되는 문자열을 찾는 `RegExp` 메소드<br />정보를 가지고 있는 `array` return (찾지 못했다면 `null` return)<br /> :exclamation:_exec와 다른 점은 match는 g 플래그가 있으면 문자열 내의 모든 값을 찾아서 return 한다._ |
| **search**  | 대응되는 문자열이 있는지 검사하는 `String` 메소드 <br />대응된 부분의 `Index` return (찾지 못했다면 `-1` return)                                                                                                      |
| **replace** | 대응되는 문자열을 찾아 다른 문자열로 치환하는 `String` 메소드                                                                                                                                                         |
| **split**   | 정규식 또는 문자열로 대상 문자열로 나누어 `array` 로 return                                                                                                                                                           |

위에서 완성한 **RegExp 패턴과 플래그**를 가지고 위 **메소드**와 함께 조합해서 사용한다.

> 보통 매칭되는 문자열이 있는지 없는지만 확인하는 용도라면 성능(속도)을 고려하여 `test`와 `search`를 이용한다.

따라서 여기서는 `exec`와 `replace`, `split`에 대해서만 정리하겠다.

#### exec

```javascript
var myRe = /d(b+)d/g;
//or
var myRe = new RegExp('d(b+)d', 'g');

var myArray = myRe.exec('cdbbdbsbz');
```

#### replace

```javascript
var re = /(\w+)\s(\w+)/;
var str = 'John Smith';
var newstr = str.replace(re, '$2, $1');
console.log(newstr);

// "Smith, John"
```

#### split

```javascript
var re = /\s/;
var str = 'I like coffee';
var splitedArr = str.split(re);
console.log(splitedArr);

// ['I', 'like', 'coffee']
```

## 정리

위에서 보듯이 사용법은 비슷비슷해서 그렇게 어렵지 않다.

사실 RegExp의 핵심은

> _"패턴을 얼마나 잘 작성하는가?"_

인 것 같다.

자주 사용할 일이 있을까 싶지만, 이번에 정리해 놓으면서 사용할 일이 생기면, 문제를 정확히 정의하고 알맞은 패턴을 짜는 데에 집중해야겠다는 생각이 든다.