## 1. 표
GFM은 마크다운에서 테이블을 사용할 수 있도록 확장 기능이 활성화되어있습니다. 표의 각 행은 파이프(|)로 구분되고, '-'로 열을 구분합니다. ':' 문자로는 정렬을 정의할 수 있습니다. '-' 기준 왼쪽에 콜론(':') 문자를 넣으면 왼쪽 정렬, 오른쪽은 오른쪽 정렬, 양 옆은 가운데 정렬입니다.

### 예제  
```
| foo | bar |
| --- | --- |
| baz | bim |
```

### 출력
| foo | bar |
| --- | --- |
| baz | bim |

<br>

표의 열 길이('-')를 일치할 필요는 없지만, 가독성을 위해 길이를 맞추는 것이 좋습니다. 마찬가지로 양 옆의 파이프('|')의 사용도 필수는 아닙니다.

### 예제  
```
| abc | defghi |
:-: | -----------:
bar | baz
```

### 출력
| abc | defghi |
:-: | -----------:
bar | baz

<br>

파이프를 행의 구분이 아닌, 문자로 사용하고 싶다면 백슬래시('\')를 앞에 붙이면 됩니다.

### 예제  
```
| f\|oo  |
| ------ |
| b `\|` az |
| b **\|** im |
```

### 출력
| f\|oo  |
| ------ |
| b `\|` az |
| b **\|** im |

<br>

표는 첫 번째 빈 라인이나 다른 블록구조의 시작 전까지 테이블로 인식합니다. 또한, 머리글 행 셀의 개수는 구분자 행과 일치해야합니다. 그렇지 않으면 표가 인식되지 않습니다.

### 예제  
```
| abc | def |
| --- | --- |
| bar | baz |
> bar

| abc | def |
| --- |
| bar |
```

### 출력
| abc | def |
| --- | --- |
| bar | baz |
> bar

| abc | def |
| --- |
| bar |

<br>

표의 나머지 행은 셀 수에 따라 다를 수 있습니다. 머리글 행의 셀 수보다 적은 셀 수가 있으면 빈 셀이 삽입됩니다. 크기가 커서 초과될 경우에는 무시됩니다.

### 예제  
```
| abc | def |
| --- | --- |
| bar |
| bar | baz | boo |
```

### 출력
| abc | def |
| --- | --- |
| bar |
| bar | baz | boo |

<br>

만약 표의 본문에 행이 없는 경우, HTML 출력에 \<tbody>가 생성되지 않습니다.

### 예제  
```
| abc | def |
| --- | --- |
```

### 출력
| abc | def |
| --- | --- |

<br><br>

## 2. 리스트 확장 기능
기존의 리스트는 순서 리스트와 기호 리스트가 있고 이를 들여쓰거나 섞어서 사용했습니다. GFM에서는 체크박스로 리스트를 나타낼 수 있습니다. 기호 리스트 이후에 대괄호("[ ]")를 표시하고 그 사이에 대문자 'X'로 구성됩니다. 이를 출력하면 선택된 체크박스를 출력합니다. 만약, 'X'를 입력하지 않으면 빈 체크박스를 출력합니다. 

HTML에서는 \<input type="checkbox">와 동일합니다. 출력결과물은 실제로 체크박스를 선택 및 선택해제하는 동적 상호 작용을 처리할 수 있습니다.

### 예제1
```
- [ ] foo
- [x] bar
```

### 출력1
- [ ] foo
- [x] bar

### 예제2
```
- [x] foo
  - [ ] bar
  - [x] baz
- [ ] bim
```

### 출력2
- [x] foo
  - [ ] bar
  - [x] baz
- [ ] bim

<br><br>

## 3. 취소선
특정 문장이나 단어를 취소선으로 나타내고 싶다면, 물결 표시('~') 두 개로 묶어 표시하면 됩니다. 주의할 점은, 새로운 단락으로 나뉘어지면 취소선이 적용되지 않습니다.

### 예제1
```
~~Hi~~ Hello, world!
```

### 출력1
~~Hi~~ Hello, world!

### 예제2
```
This ~~has a

new paragraph~~.
```

### 출력2
This ~~has a

new paragraph~~.

<br><br>

## 4. 자동링크
마크다운에서 링크를 입력하려면 꺾쇠괄호로 URL을 묶어서 링크를 삽입합니다. 하지만 GFM에서는 더 많은 상황에서 링크를 인식하여 활성화합니다. 

꺾쇠괄호 없이 URL을 입력해도 링크로 인식합니다.

### 예제
```
Visit www.commonmark.org/help for more information.
```

### 출력
Visit www.commonmark.org/help for more information.

<br>
<br>

자동링크에 '?', '!', '.', ',', ':', '*', '_', '~'은 링크 내부에 포함될 수 있지만 일반적으로 자동 링크의 일부로 간주되지 않습니다.

### 예제
```
Visit www.commonmark.org.

Visit www.commonmark.org/a.b.
```

### 출력
Visit www.commonmark.org.

Visit www.commonmark.org/a.b.

<br><br>

자동링크가 ')'로 끝나면, 전체 자동링크에서 총 괄호의 수를 검사합니다. 여는 괄호보다 닫는 괄호가 더 많은 경우에는 괄호 안에 자동 링크를 쉽게 포함하기 위해 수가 안맞는 괄호 뒤부분은 고려하지 않습니다. 만약 괄호가 자동링크 내부에 있다면 해당 규칙을 적용하지 않습니다.

### 예제
```
www.google.com/search?q=Markup+(business)

www.google.com/search?q=Markup+(business)))

(www.google.com/search?q=Markup+(business))

(www.google.com/search?q=Markup+(business)
```

### 출력
www.google.com/search?q=Markup+(business)

www.google.com/search?q=Markup+(business)))

(www.google.com/search?q=Markup+(business))

(www.google.com/search?q=Markup+(business)

<br><br>

자동링크가 세미콜론(';')으로 끝나는 경우에는 앞에 텍스트가 엔퍼센트('&')이고, 그 뒤에 하나 이상의 영숫자가 오는 경우, 자동 링크에서 제외됩니다.

### 예제
```
www.google.com/search?q=commonmark&hl=en

www.google.com/search?q=commonmark&hl;
```

### 출력
www.google.com/search?q=commonmark&hl=en

www.google.com/search?q=commonmark&hl;

<br><br>

자동링크는 "http://"와 "https://" 둘다 적용이 되고, 유효성 검사에 따라 공백이 아니고 '<' 문자가 아닐 경우에만 링크로 인식합니다.

### 예제
```
www.commonmark.org/he<lp

http://commonmark.org

(Visit https://encrypted.google.com/search?q=Markup+(business))
```

### 출력
www.commonmark.org/he<lp

http://commonmark.org

(Visit https://encrypted.google.com/search?q=Markup+(business))

<br><br>

링크와 마찬가지로, 이메일 역시 GFM에서 자동으로 인식 가능합니다. 이메일 자동링크는 다음의 규칙을 따릅니다.

- 영숫자, '.', '-', '_', '+'가 한글자 이상이어야합니다.
- '@' 기호가 포함되어야 합니다.
- 마침표('.')로 구분된 한글자 이상의 영숫자나 '-', '\_'가 있어야합니다. 이때, 마지막 문자는 '-'나 '\_'가 아니어야합니다.
- '@' 기호 이전에 '+'은 추가할 수 있지만, 그 이후에는 추가할 수 없습니다.

### 예제
```
foo@bar.baz  

hello@mail+xyz.example 은 유효하지 않지만, hello+xyz@mail.example 은 유효합니다.

```

### 출력
foo@bar.baz  

hello@mail+xyz.example 은 유효하지 않지만, hello+xyz@mail.example 은 유효합니다.  

<br><br><br><br>

'.', '-', '_' 문자는 '@' 기호의 양쪽에 나타날 수 있습니다. 마침표('.')는 이메일 주소의 끝에서 사용할 수 있지만, 이 경우에는 주소의 일부로 간주되지 않습니다.

### 예제
```
a.b-c_d@a.b

a.b-c_d@a.b.

a.b-c_d@a.b-

a.b-c_d@a.b_

```

### 출력
a.b-c_d@a.b

a.b-c_d@a.b.

a.b-c_d@a.b-

a.b-c_d@a.b_  
<br><br>

## 5. HTML 태그 비활성화
GFM에서는 다음 HTML 태그를 필터링하여 HTML로 출력되지 않고, 태그 그대로 출력됩니다.

- <title>
- <textarea>
- <style>
- <xmp>
- <iframe>
- <noembed>
- <noframes>
- <script>
- <plaintext>

### 예제
```
<strong> <title> <style> <em>

<blockquote>
  <xmp> 은 필터링됩니다.  <XMP> 역시 필터링됩니다.
</blockquote>

```

### 출력
<strong> <title> <style> <em>

<blockquote>
  <xmp> 은 필터링됩니다.  <XMP> 역시 필터링됩니다.
</blockquote>
