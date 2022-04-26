마크다운(Markdown) 문법
===


# 1. 마크다운에 관하여
## 1.1. 마크다운이란?
마크다운(Markdown)은 2004년John Gruber와 Aaron Swartz에 의해 개발된 경량형 마크업 언어이다. 깃허브의 **README.md** 파일에서 자주 볼 수 있으며, 어떤 개발자인지 상관없이 대부분의 개발자들이 일상생활에서 사용하는 언어이다.
   
   
   
## 1.2. 마크다운 문법 (Markdown_syntax)
### 1.2.1. Headings
```
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6
```
   

### 1.2.2. Line


```
***
*****
---
-----
___
```

### 1.2.3. Styling text
|Style|Syntax|
|:--:|:--:|
|Bold|`** **` or `__ __`|
|Italic|`* *` or `_ _`|
|Strikethrough|`~~ ~~`|
|Bold and nested italic|`** **` and `_ _` |
|All bold and italic|`*** ***`|
    
### 1.2.4. How to make list

- 순서가있는 리스트 (번호)
```
1. 첫번째
3. 세번째
2. 두번째
```
어떤 번호를 입력해도 순서는 오름차순으로 정렬된다.   

- 순서가 없는 리스트 (`*`,`+`,`-` 지원)
```
* 첫번째
  * 두번째
    * 세번째

+ 첫번째
  + 두번째
    + 파랑

- 첫번째
  - 두번째
    - 세번째
```
탭을 사용하여 리스트를 세분화할 수 있다.

- Task List
```
[x] task 1
[ ] task 2
```
- [x] task 1
- [ ] task 2

### 1.2.5. How to make Table
```
|Column_1|Column_2|
|:--:|:--:|
|Value_1|Value_2|
|Value_1|Value_2|
|Value_1|Value_2|
```

:로 정렬을 할 수 있다.   

### 1.2.6. quoting text
```
> This is first sentence
>> This is second sentence
>>> This is third sentence
```
> This is first sentence   
>> This is second sentence   
>>> This is third sentence   

### 1.2.7. quoting code

- 코드가 한줄일때, 코드블럭코드("\``")을 이용한다
<pre>
<code>
`code`
</code>
</pre>

- 코드가 여러줄일때, 코드블럭코드("\```")을 이용한다
<pre>
<code>
```
code
```
</code>
</pre>
코드블럭("\```") 시작점에 사용하려는 언어를 선언하면 **문법강조(Syntax highlighting)**이 가능하다.

- `<pre><code></code></pre>`을 이용한다
```
<pre>
<code>
code what you want
</code>
</pre>
```


### 1.2.8. Link
```
[description](link)
```

### 1.2.9. Images
- 이미지 링크를 입력한다
```
![This is an image](image link)
```
- html 태그기능을 활용한다 (크기 설정 가능)
```
<img src="image_link" width="400" height="300">
```

### 1.2.10. Ignoring Markdown formatting
`\`를 사용한다.

### 1.2.11. How to begin a new line
3칸 이상 띄어쓰기(`  `)하면 줄이 바뀐다.


## ○ 레퍼런스
* [ihoneymon님의 마크다운 작성법](https://gist.github.com/ihoneymon/652be052a0727ad59601)
* [드림코딩 마크다운](https://www.youtube.com/watch?v=kMEb_BzyUqk)
* [GitHub Docs](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
