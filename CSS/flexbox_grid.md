## 등장배경
FlexBox와 CSS Grid 등장 이전에 css로 웹 페이지 레이아웃을 배치하기 위해서는 table, float, position, inline-block 등의 방법을 사용했지만 레이아웃을 어찌저찌 만들순 있어도 올바르게 배치하는 방법들은 아니었다. 이런 문제들을 해결하고 더 완벽한 레이아웃을 만들기 위해 FlexBox Grid가 만들어졌다. 둘 다 IE(10,11버전은 일부 지원)를 제외하고는 모든 브라우저에서 지원한다.

## FlexBox

FlexBox 레이아웃은 크기를 알 수 없고 동적인 레이아웃 요소들의 배치, 정렬을 보다 효율적으로 하기 위해 고안되었다. flex라는 이름대로 유연하게 컨테이너를 조정할 수 있지만 소규모 레이아웃 및 구성요소에 사용하기에 가장 적합하며 대규모 레이아웃에는 Grid 레이아웃이 적합하다.

#### 기본 개념
FlexBox는 container와 item으로 구성되있다. container는 부모 요소이고 display:flex가 선언되며 item은 그 container의 자식 요소이다. 일반 레이아웃의 흐름 방향과는 다르게 flex-direction으로 흐름 방향이 결정된다. item은 flex-direction에 따라 배치된다.
* flex container : display:flex를 선언하는 flex item들의 부모 요소
* flex item : flex container의 자식 요소
* flex direction : flex item들의 진행 방향

## CSS Grid
CSS Grid layout은 이전 웹 페이지 레이아웃 시스템과 비교하여 UI를 설계하는 방식과는 다른 2차원 grid기반 레이아웃 시스템이다. FlexBox는 1차원 레이아웃 시스템이다.

#### 기본 개념
FlexBox처럼 container에 display:grid를 선언하고 행,열 크기는 gird-template-rows, grid-template-columns로 설정하고 자식 요소는 grid-row, grid-column으로 배치한다.
* grid container : display:grid를 선언하는 grid item들의 부모요소
* grid item : grid container의 자식 요소
* grid line : grid 구조를 구성하는 구분선
* grid cell : grid의 단일 단위. 한 칸
* grid track : grid의 행 또는 열. 한 줄
* grid area : grid cell의 집합

<br/>

>[CSS TRICKS - A Complete Guide to FlexBox](https://css-tricks.com/snippets/css/a-guide-to-FlexBox/#top-of-site)<br/>
[CSS TRICKS - A Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/#top-of-site)