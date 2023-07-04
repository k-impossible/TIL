## Combinators
* 후손 셀렉터 ``div p {...}``
div 안에 있는 모든 p를 선택한다.

* 자식 셀렉터 ``div > p {...}``
div가 부모 요소인 p를 선택한다.

* 인접 형제 셀렉터 ``div + p {...}``
같은 부모를 가지면서 div의 바로 뒤에 나오는 첫번째 p를 선택한다.

* 형제 셀렉터 ``div ~ p {...}``
같은 부모를 가지면서 div의 뒤에 나오는 모든 p를 선택한다.

## 가상 클래스 셀렉터
* :empty ``p:empty {...}``
비어있는 모든 p를 선택한다.

* :not(selector) ``:not(p) {...}``
p가 아닌 모든 요소를 선택한다.

* :first-child ``p:first-child {...}``
부모 요소에서 첫번째 자식인 p를 선택한다.

* :first-of-type ``p:first-of-type {...}``
부모 요소에서 첫번째로 나오는 p를 선택한다.

* :last-child ``p:last-child {...}``
부모 요소에서 마지막 자식인 p를 선택한다.

* :last-of-type ``p:last-of-type {...}``
부모 요소에서 마지막에 나오는 p를 선택한다.

* :nth-child(n) ``p:nth-child(2) {...}``
부모 요소에서 2번째 자식인 p를 선택한다.
``p:nth-child(4n+0){...}`` 4의 배수 선택
``p:nth-child(-n+4){...}`` 4번째 까지 선택
``p:nth-child(odd){...}`` 홀수번째 선택
``p:nth-child(even){...}`` 짝수번째 선택

* :nth-of-type(n) ``p:nth-of-type(2) {...}``
부모 요소에서 2번째로 나오는 p를 선택한다.

* :nth-last-child(n) ``p:nth-last-child(2) {...}``
부모 요소에서 마지막부터 2번째 자식인 p를 선택한다.

* :nth-last-of-type(n) ``p:nth-last-of-type(2) {...}``
부모 요소에서 마지막부터 2번째로 나오는 p를 선택한다.

* :only-of-type ``p:only-of-type {...}``
부모 요소에서 유일한 p를 선택한다.

* :only-child ``p:only-child {...}``
부모 요소에서 유일한 자식인 p를 선택한다.

## 가상 요소 셀렉터
* ::after ``p::after {...}``
p의 뒤에 컨텐츠를 삽입한다.

* ::before ``p::before {...}``
p의 앞에 컨텐츠를 삽입한다.

* ::first-letter ``p::first-letter {...}``
p의 첫번째 문자를 선택한다.

* ::first-line ``p::first-line {...}``
p의 첫번째 줄을 선택한다.

` ::first-letter와, ::first-line은 블록 레벨의 요소에만 적용된다.` <br>
`적용할 수 있는 속성 : font, color, background, margin, padding, border, text-decoration, vertical-align, line-height, float, clear`

* ::marker ``::marker {...}``
list item의 마커를 선택한다.

* ::selection ``::selection {...}``
유저가 선택(드래그)한 요소를 선택한다. 
적용할 수 있는 속성 : color, background, cursor, outline

<br>

>[w3schools - css selectors](https://www.w3schools.com/css/css_selectors.asp)<br/>
[MDN - Pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child)

