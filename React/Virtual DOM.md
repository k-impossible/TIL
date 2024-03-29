## Virtual DOM
React는 UI의 상태를 추적하고 변화가 일어난 요소들을 빠르게 업데이트할 수 있도록 Virtual DOM이라는 가상의 DOM객체를 활용한다. 이는 실제 DOM의 사본 같은 개념으로 React는 실제 DOM 객체에 접근하여 조작하는 대신 가상의 DOM 객체에 접근하여 변화 전과 후를 비교하고 바뀐 부분을 적용한다.
### DOM의 조작 속도가 느려지는 이유
브라우저는 렌더링 과정에서 DOM 트리와 CSSOM 트리를 토대로 Render 트리를 생성하고 각 요소가 배치될 공간을 계산(Layout)한 뒤 이를 화면에 그려낸다.(Paint) 만약 DOM이 변경된다면 업데이트된 요소와 그에 해당하는 자식 요소들에 의해 DOM 트리를 재구축하게 된다.그 과정에서 이에 대한 레이아웃 재연산을 수행하는 리플로우, 화면에 그려내는 Repaint 과정을 거치게 된다. 이때 변화가 필요 없는 부분도 변경되면서 잦은 리플로우 발생으로 인해 성능을 떨어뜨리는 문제를 야기하게 된다. 따라서 Javascript를 통한 DOM 조작이 많아질수록 이에 대한 리플로우가 발생하므로 DOM 업데이트 비용이 커질 수 있다.
### Virtual DOM의 형태
가상 DOM은 추상화된 자바스크립트 객체의 형태를 가지고 있다. 실제 DOM과 마찬가지로 가상 DOM 또한 HTML 문서 객체를 기반으로 한다. 추상화만 되었을 뿐 평범한 자바스크립트 객체이므로 실제 DOM을 건드리지 않고도 필요한 만큼 자유롭게 조작할 수 있다. 가상 DOM은 리액트에서 컴포넌트의 상태나 속성이 변경될 때마다 새로 생성되며 리액트는 이전 가상 DOM과 새로운 가상 DOM을 비교하여 변경된 부분만 실제 DOM에 반영한다.
### Virtual DOM의 동작 과정
리액트는 상태를 변경하는 작업이 일어났을 때 가상 DOM에 저장된 이정 상태와 변경된 현재 상태를 비교한다. 이 비교 과정에서 리액트는 Diffing 알고리즘을 사용하여 변경된 부분을 감지한다. 상태를 변경하는 경우에는 Diffing 알고리즘에서 이를 감지할 수 있도록 직접 할당이 아닌 `setState`와 같은 메서드를 활용해 상태를 변경한다. 
- Reconciliation(재조정) : 가상 DOM과 변경된 새로운 가상 DOM을 비교해 변경이 필요한 부분만 실제 DOM에 반영하여 업데이트하는 과정
- Batch Update(일괄 업데이트) : 여러 개의 상태 변화가 있을 경우 일일이 업데이트를 하지 않고 일괄적으로 한 번에 업데이트하는 과정. 이를 통해 성능을 최적화하고 불필요한 렌더링을 최소화할 수 있다.

<br/>

## React Diffing Algorithm
React는 하나의 트리를 다른 트리로 변형을 시키는 가장 작은 조작 방식을 알아내야만 했는데 두 가지의 가정을 가지고 시간 복잡도 O(n)의 새로운 휴리스틱 알고리즘(Heuristic Algorithm)을 구현해낸다.
- 각기 서로 다른 두 요소는 다른 트리를 구축할 것이다.
- 개발자가 제공하는 `key`프로퍼티를 가지고 여러 번 렌더링을 거쳐도 변경되지 말아야 하는 자식 요소가 무엇인지 알아낼 수 있을 것이다.
이 두 가정은 거의 모든 실제 사용 사례에 들어맞게 된다. 여기서 리액트는 비교 알고리즘(Diffing Algorithm)을 사용한다.
### React가 DOM 트리를 탐색하는 방법
리액트는 기존의 가상 DOM 트리와 새롭게 변경된 가상 DOM 트리를 비교할 때 트리의 레벨 순서대로 순회하는 방식으로 탐색한다. 이는 너비 우선 탐색(BFS)의 일종이라고 볼 수 있다. 동일 선상에 있는 노드를 파악한 뒤 다음 자식 세대의 노드를 순차적으로 파악해 나간다.
#### 다른 타입의 DOM 엘리먼트인 경우
DOM 트리는 각 HTML 태그마다 각각의 규칙이 있어 그 아래 들어가는 자식 태그가 한정적이라는 특징이 있다. 자식 태그의 부모 태그 또한 정해져 있다는 특징이 있기 때문에 부모 태그가 달라진다면 리액트는 이전 트리를 버리고 새로운 트리를 구축한다. 새로운 컴포넌트가 실행되면서 기존의 컴포넌트는 완전히 해제(Unmount)되어버리기 때문에 기존의 state 또한 파괴된다.
#### 같은 타입의 DOM 엘리먼트인 경우
반대로 타입이 바뀌지 않는다면 리액트는 최대한 렌더링을 하지 않는 방향으로 최소한의 변경 사항만 업데이트한다. 이렇게 수정된 요소만 처리한 뒤 리액트는 뒤이어서 해당 노드들 밑의 자식들을 순차적으로 동시에 순회하면서 차이가 발견될 때마다 변경한다. 이를 '재귀적으로 처리한다'고 표현한다.
#### 자식 엘리먼트의 재귀적 처리
리액트는 위에서 아래로 순차적으로 비교하기 때문에 이 동작 방식에 대해 고민하지 않고 처리하게 되면 이전의 코드에 비해 훨씬 나쁜 성능을 내게 된다.
```html
<ul>
  <li>A</li>
  <li>B</li>
</ul>

<ul>
  <li>C</li> // 추가
  <li>A</li>
  <li>B</li>
</ul>
```
처음의 자식 노드를 비교할 때 `A`,`C`가 서로 다르다고 인지하게 된 리액트는 리스트 전체가 바뀌었다고 받아들인다. `A`,`B`는 그대로이기 때문에 두 자식 노드는 유지시켜도 된다는 것을 깨닫지 못하고 전부 버리고 새롭게 렌더링 해버린다. 그래서 리액트는 이 문제를 해결하기 위해 `key` 속성을 지원한다.
#### 키(key)
만약 자식 노드들이 `key`를 갖고 있다면 리액트는 이를 이용해 기존 트리의 자식과 새로운 트리의 자식이 일치하는지 아닌지 확인할 수 있다. 키 속성에는 보통 DB상의 유니크한 값을 부여해 주면 된다. 키는 전역적으로 유일할 필요는 없고 형제 엘리먼트 사이에서만 유일하면 된다. 만약 유니크한 값이 없다면 배열의 인덱스를 키로 사용할 수 있지만 배열이 다르게 정렬될 경우가 생긴다면 배열의 인덱스를 키로 선택했을 경우 비효율적으로 동작할 것이다. 왜냐하면 배열이 다르게 정렬되어도 인덱스는 그대로 유지되기 때문이다. 인덱스는 그대로지만 그 요소가 바뀌어버린다면 리액트는 배열의 전체가 바뀌었다고 받아들이고 새로운 DOM 트리를 구축해버리기 때문에 비효율적으로 동작하는 것이다.