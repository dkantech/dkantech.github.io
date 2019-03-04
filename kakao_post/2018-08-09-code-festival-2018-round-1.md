---
layout: post
title: '코드 페스티벌 2018 예선전 이야기'
author: bryan.j
date: 2018-08-09 17:00
tags: [code-festival, programming-contest, coding]
image: /files/covers/code-festival-2018-round-1.png
---
## 카카오 코드 페스티벌 예선전, 많은 관심 감사합니다! 

작년에 이어 두 번째로 진행된 카카오 코드 페스티벌, 온라인 예선이 지난 8월 4일 토요일에 진행됐습니다. 작년보다 더욱 많은 6,000여 명의 참가자들이 6시간 동안 뜨거운 열정을 발휘했는데요, 특히 실시간으로 바뀌는 스코어보드를 보면서 치열한 접전을 느낄 수 있었습니다. 여기 예선 문제와 해설, 그리고 결과를 공유합니다. 참가해주신 모든 모든 분들께 감사드립니다!

## 문제 설명 및 풀이

### 상금 헌터

- 제출자 3120명
- 정답자 2686명
- [문제 풀러 가기](https://www.acmicpc.net/problem/15953){:target="_blank"}

대회에 참가해서 얼마의 상금을 받을 수 있을지를 계산하는 문제로, 주어진 조건대로 구현하면 됩니다. `if`문을 사용해서, a와 b가 어떤 범위가 있는지에 따라 상금을 구하거나, 크기가 101인 배열 `A[0..101]`와 65인 배열 `B[0..64]` 두 개를 만들어서, 각각 1회/2회 대회에서 i등을 하면 얼마의 상금을 받는지를 저장한 뒤 계산하는 방법 등이 있습니다.

### 인형들

- 제출자 2138명
- 정답자 942명
- [문제 풀러 가기](https://www.acmicpc.net/problem/15954){:target="_blank"}

길이가 N인 수열이 주어졌을 때, 이 중 K개 이상의 연속된 수를 선택하여 표준편차를 최소로 만드는 문제입니다. 범위가 작기 때문에 정의된 대로 직접 계산해도 되고, 이를 좀 더 효율적으로 계산할 수도 있습니다.

**Naive: O(N<sup>3</sup>)**

모든 경우를 다 고려하여 구현해보는 방법입니다. j - i + 1 &ge; K, 1 &le; i, j &le; N 을 만족하는 모든 i, j에 대해서 다음과 같은 과정을 수행하면 됩니다.

- m = (a[i] + a[i+1] + ... + a[j]) / N
- v = ((a[i] - m) * (a[i] - m) + ... + (a[j] - m) * (a[j] - m)) / N

참고로, 여기서 m, v는 각각 (산술) 평균과 분산을 의미하며, 문제에 나와있는 식과 같습니다.  그 후 구한 v 중에서 최솟값을 구하고 이 값의 음이 아닌 제곱근을 출력하면 됩니다.

가능한 (i, j)의 가짓수가 O(N<sup>2</sup>)이므로, 모든 (i, j)에 대하여 평균과 분산을 구하는 프로그램의 시간복잡도는 O(N<sup>3</sup>)이 됩니다. 

**O(N<sup>2</sup>)**

(분산) = (제곱의 평균) - (평균) * (평균) 이라는 성질이 알려져 있습니다. 그러므로 누적 합 배열과 제곱의 누적 합 배열을 만들면, j - i + 1 &ge; K, 1 &le; i, j &le; N 을 만족하는 모든 i, j에 대해서 평균과 분산을 O(1)의 시간에 구할 수 있습니다.

가능한 (i, j)의 가짓수가 O(N<sup>2</sup>)이므로, O(N<sup>2</sup>)의 시간복잡도로 문제를 풀 수 있습니다.

그 외에 추가로 고려해야 할 사항은 다음과 같습니다.
- 인형을 K개를 선택하는 것이 아니라 K개 이상을 선택해야 한다는 점이 있는데, 의도하지 않게 많은 분들이 처음에 이러한 것을 간과한 것으로 보입니다.
- 절대/상대 오차가 10<sup>-6</sup>이므로, 실수의 정밀도 관련 문제에 대해 어느 정도 고려할 필요가 있습니다.
  - C++ 기준으로, float를 이용하여 O(N<sup>3</sup>)을 적용하면 정답을 받지 못합니다. double / long double을 사용하면 정답을 받을 수 있습니다.
  - 최대한 실수 연산의 수를 줄이는 것이 좋습니다. 예를 들어, 평균을 구할 때에는 수들의 합을 정수형 변수에 저장한 후 N으로 나누는 것이 실수형 변수를 이용하여 연산하는 것에 비해서 좀 더 정확하게 구할 수 있습니다.
- Python으로 구현하는 경우, 다른 언어들에 비해 실행 시간이 더 걸리기 때문에, O(N<sup>3</sup>) 풀이를 구현하면 시간 초과를 받게 될 수 있습니다.

### 숏코딩

- 제출자 235명
- 정답자 50명
- [문제 풀러 가기](https://www.acmicpc.net/problem/15956){:target="_blank"}

문제의 조건에 맞게 생성된 논리식이 입력되었을 때, 이 식과 동치인 논리식 중 가장 짧은 논리식을 찾는 문제입니다. `==`과 `!=`를 나누어 생각합니다.
- `==`:  각 단항식을 정점으로, `<X>==<Y>`를 `<X>`와 `<Y>`를 잇는 양방향 간선으로 생각한 그래프에서 한 컴포넌트에 속한 정점들은 모두 값이 같아야 합니다. 이는 `==`가 동치관계(equivalence relation)이기 때문입니다.
  - 한 컴포넌트에 있는 단항식들을 u<sub>1</sub>, u<sub>2</sub>, ..., u<sub>n</sub>이라고 하고, 그 중 길이가 가장 짧은 것을 u<sub>i</sub>라고 하면, u<sub>i</sub>와 다른 모든 정점을 잇는 n-1개의 간선만 있어도 정점들을 똑같이 묶을 수 있고, 이렇게 하는 것이 가장 길이가 짧습니다. 컴포넌트의 크기가 1이라면 (`1==1`, `a==a` 등으로 가능) 그 컴포넌트는 출력에 포함되지 않아야 합니다.
  - 단, 같은 컴포넌트에 2개 이상의 **정수**가 있다면, 조건문은 항상 `false`를 반환합니다.
- `!=`: `<X>!=<Y>`가 있다고 가정하면,
  - `<X>`와 `<Y>`를, 같은 `==` 컴포넌트에 속한 가장 길이가 짧은 단항식으로 교체할 수 있습니다.
  - (교체한 이후) 똑같은 `!=` 조건문이 여러 개 있다면 그 중 하나만 남겨둘 수 있습니다.
  -  `<X>`와 `<Y>`가 같은 `==` 컴포넌트에 속한다면, 조건문은 항상 `false`를 반환하므로, 이와 동치인 가장 짧은 조건문(ex: `x!=x`, `4==7`)을 출력해야 합니다.
  - `<X>`가 속하는 `==` 컴포넌트에 정수가 포함되어 있고, `<Y>`가 속하는 `==` 컴포넌트에도 정수가 포함되어 있다면, 해당 비교 연산은 결국 서로 다른 두 정수를 비교하고 있으므로 필요가 없고, 따라서 제거할 수 있습니다.

위의 과정에서 비교 연산들이 모두 불필요하다고 판단되어 제거되었다면, 조건문은 항상 `true`를 반환하는 식이 됩니다.  항상 `true`나 `false`를 반환하는 가장 짧은 조건문은 길이가 4이며, 각각 `T==T`와 `0!=0`의 예시가 있습니다.

### 부스터

- 제출자 603명
- 정답자 102명
- [문제 풀러 가기](https://www.acmicpc.net/problem/15955){:target="_blank"}

N개의 체크포인트 사이를 규칙에 맞게 이동하는 방법이 있는지를 찾는 문제입니다. 체크포인트의 수와 질의의 수 모두 최대 25만 개로 매우 많으므로 단순한 방법으로는 시간 안에 답을 구하기가 매우 힘들기 때문에, 다음과 같이 단계별로 알고리즘을 개선시켜볼 수 있습니다.

**O(QN<sup>2</sup>)**

문제를 있는 그대로 해석하면, 각각의 체크포인트에서 HP 재충전 / 부스터 재충전 여부를 모두 저장해야 하는 아주 복잡한 문제가 됩니다. 이 정보들을 최대한 간소화할 수 있을까요?

- **각각의 체크포인트에서 HP / 부스터의 재충전 여부를 기억할 필요가 없습니다.**  어떠한 체크포인트에 두 번 이상 방문하는 경로가 있다면, 그 체크포인트를 마지막으로 빠져나간 방법을 처음부터 사용하면 됩니다. 그렇다면 임의의 체크포인트에는 많아야 한 번만 방문해도 답을 찾을 수 있고, 이 때 HP / 부스터를 재충전하지 않아서 손해를 볼 일이 없습니다. 고로, 체크포인트에 방문했다는 것은 HP / 부스터를 재충전했다는 것과 동일합니다.
- 체크포인트 간을 이동할 때 부스터는 많아야 한 번밖에 쓸 수 없는데, 처음에 부스터를 무조건 켜도 손해를 보지 않습니다. 처음에 걸어간 후 부스터를 사용하는 경로는, 똑같이 평행이동 시켜서 처음에 부스터를 사용한 후 걸어가는 경로로 바꿔줄 수 있기 때문입니다. 고로 처음에 부스터를 잘 켜서 걷는 거리를 최소화하는 문제인데, X좌표와 Y좌표 차 중에서 큰 쪽을 줄여나가는 전략이 유효하므로, **두 체크포인트 (X<sub>u</sub>, Y<sub>u</sub>)와 (X<sub>v</sub>, Y<sub>v</sub>)를 오갈 때 걸어가야 하는 최소 거리는 min(\|X<sub>u</sub> - X<sub>v</sub>\|, \|Y<sub>u</sub> - Y<sub>v</sub>\|)입니다.** 

이 관찰을 통해서 문제는 그래프 탐색 문제로 환원됩니다. 각각의 쿼리가 주어졌을 때, min(\|X<sub>u</sub> - X<sub>v</sub>\|, \|Y<sub>u</sub> - Y<sub>v</sub>\|)가 주어진 HP 제한 이하인 쌍에 대해서 양방향 간선이 있다고 생각하고, 깊이 우선 / 너비 우선 탐색을 사용해서 문제를 해결할 수 있습니다. 시간 제한을 맞추기에는 너무 느린 알고리즘이지만, 좋은 시작점으로 삼을 수 있겠죠.

**O(N log N + QN)**

현재 사용하는 방법의 문제점 중 하나는, 고려해야 할 간선의 개수가 O(N<sup>2</sup>)개에 육박할 정도로 많다는 것입니다. 이를 줄이기 위해서는 다음과 같은 아이디어가 필요합니다.

일단, 간선을 이을 때 min(\|X<sub>u</sub> - X<sub>v</sub>\|, \|Y<sub>u</sub> - Y<sub>v</sub>\|) 비용의 간선 하나를 잇는 대신 \|X<sub>u</sub> - X<sub>v</sub>\|, \|Y<sub>u</sub> - Y<sub>v</sub>\| 비용의 간선 두개를 잇는다고 생각해 봅시다. 이렇게 해도 둘 중 비용이 적은 간선을 고를 것이기 때문에 답에는 변화가 없고, 식은 단순해 집니다.

위 그래프에서 X좌표 차이로 이루어진 간선들만 생각해 봅시다. 그러한 간선들만 놓고 보았을 때 Y좌표는 중요한 요인이 아니기 때문에, 우리는 X축 수직선에 점들을 찍어놓고, 두 점의 거리차로 간선을 이었다고 생각할 수 있습니다. 그렇다면, 수직선 상에 인접하지 않은 두 점 간에 간선을 이을 필요가 있을까요? 인접한 정점을 타고서도 해당 위치로 도달할 수 있기에, 굳이 큰 가중치를 사용해서 수직선 상에 인접하지 않은 두 점을 오갈 필요가 없습니다. 

같은 이야기는 Y좌표 차이로 이루어진 간선들에 대해서도 똑같이 적용됩니다. 이로써 얻을 수 있는 결론은 다음과 같습니다.

"**X좌표 순으로 정렬했을 때 인접한 N-1개의 쌍과, Y좌표 순으로 정렬했을 때 인접한 N-1개의 쌍만 고려해도 된다.**"

이제, 각각의 좌표로 정렬한 후, 인접한 쌍에 대해서만 간선을 이어주면 된다는 결론에 도달합니다. 그래프의 크기가 작아졌으니, 훨씬 더 문제를 해결하기 수월해졌죠. 물론, 여전히 탐색을 일일이 해 주기에는 쿼리의 수가 너무 많습니다.

**O(N log N + Q log Q)**

복잡도를 줄이는 전략이 여러 가지가 있으나, 이 중 가장 간단한 전략은 모든 쿼리를 X의 오름차순으로 정렬하는 것입니다. 결국 각각의 쿼리가 의미하는 바는, **가중치 X 이하인 간선들만 사용해서 두 정점을 오갈 수 있나?** 라는 형태의 질문과 동일합니다. 이 때 모든 쿼리를 X의 오름차순으로 정렬했다면, 각각의 쿼리에서 보게 되는 간선들의 집합이 갈수록 커지게 됩니다. 

간선들이 추가되는 상황에서 두 정점을 오가는 경로가 있는지, 즉 두 정점이 연결되어 있는지를 확인하는 좋은 자료구조로는 유니온 파인드(Union-Find, 서로소 집합Disjoint Set이라고도 합니다)가 있습니다. 가중치 순서대로 모든 간선과 쿼리를 보면서, 간선이 나오면 두 정점을 하나의 집합으로 합쳐주고, 쿼리가 나오면 두 정점이 같은 집합에 있는지를 보면 됩니다. 이 방법을 사용하면 O(Q log Q) 정렬 이후 각각의 쿼리를 O(log N) 정도의 속도로 해결할 수 있습니다. 

쿼리를 정렬하지 않고 그때 그때 결과를 알아내는 방법도 있습니다. 이 방법은 그래프의 최소 스패닝 트리(Minimum Spanning Tree)에 속하는 간선만이 중요하다는 사실에 기반합니다. 해당 사실을 사용하면, 주어진 쿼리는 **트리 상의 어떠한 경로에 있는 간선들의 가중치가 모두 X 이하인가?** 라는 문제로 변환되며, 이는 트리의 경로에 대한 최댓값을 빠르게 구하는 자료구조를 O(N log N)에 만들어 놓으면, 각각의 쿼리 당 O(log N)에 해결할 수 있습니다. 조금 더 어려운 도전이 필요하다면 시도해 보셔도 좋습니다. :)

### 음악 추천

- 제출자 211명
- 정답자 34명
- [문제 풀러 가기](https://www.acmicpc.net/problem/15957){:target="_blank"}

추천이 여러 번 이루어지고 각각의 추천마다 여러 개의 노드의 값을 갱신하는 과정을 반복할 때, 지정된 값을 넘는 시점이 언제인지를 판단하는 문제입니다. 추천 횟수는 최대 10만 번이고 각각에 대해 값이 갱신되는 노드가 최대 10만 개이므로 단순히 값을 하나씩 갱신하는 방식으로는 시간 안에 답을 구할 수 없습니다.

트리 형태로 데이터가 주어지고, 서브트리 내의 모든 값에 일정한 값을 더하는 질의를 처리하기 위해서는 트리를 깊이 우선 탐색으로 방문하는 순서대로 원소를 나열하는 트리 순회 배열(Tree Traversal Array)을 만들고, 구간 트리(Segment Tree)를 사용하여 서브트리에 대응되는 구간의 값을 갱신하는 방식을 일반적으로 사용합니다.

특정 시점에 노드에 부여된 가중치를 구하는 과정은 노드마다 O(log N) 시간이 걸리기 때문에, 갱신이 이루어질 때마다 가중치의 합을 구하는 방식은 매우 비효율적입니다. 가중치의 합이 목표 점수를 언제 넘게 되는지만 구하면 되기 때문에, 목표 점수를 넘는 시간에 대한 이분 탐색을 진행할 경우, 특정한 가수의 평균 점수가 목표 점수를 넘는 시간을 O((K log N + N' log N)log T) 시간에 계산할 수 있습니다. 이 때 N'은 해당 가수가 부른 곡의 수, 즉 노드의 개수이고 T는 시간의 최대 범위인 10<sup>9</sup>입니다.

문제에서는 각 가수 별로 목표 점수를 넘게 되는 시점을 구해야 하므로, 위 과정을 모든 가수에 대해 반복할 경우 시간 안에 답을 구하기 힘듭니다. 이때 사용할 수 있는 방법이 병렬 이분 탐색(Parallel Binary Search)입니다. 이분 탐색은 구하는 값의 상한과 하한을 정한 다음 구간의 길이를 반으로 줄여나가는 과정을 반복하는 방법인데요, 구하는 값이 여러 개인 경우 각각에 대해 상한과 하한을 저장하는 배열을 정의한 뒤 한 번 계산할 때마다 모든 구간을 각각의 범위에 맞게 절반씩 줄여나갑니다. 그러면 가수의 평균 점수를 계산하는 과정은 각 가수별로 진행해야 하지만 가중치를 부여하는 과정은 여러 번 반복할 필요가 없기 때문에 모든 가수에 대해 답을 계산하는 데 걸리는 시간이 O((K log N + N log N)log T)가 됩니다. 위 식과 비교하면 값을 갱신하는 과정의 시간 복잡도는 O(K log N log T)로 같으며, 가수별로 부른 곡의 수의 합이 N이 되므로 합을 계산하는 과정의 전체 시간이 O(N log N log T)가 됨을 알 수 있습니다.

### 프로도의 100일 준비

- 제출자 122명
- 정답자 7명
- [문제 풀러 가기](https://www.acmicpc.net/problem/15958){:target="_blank"}

L-모양 직각다각형은 반드시 └ 또는 ┘ 모양이어야 하며, 밑변이 x축에 붙어 있어야 합니다. 이는 주어진 도형이 히스토그램 모양이기 때문입니다.┌ 또는 ┐ 모양이 가능하다면 넓이가 더 넓은 직사각형도 가능하고, 밑변이 x축보다 위에 있다면 도형을 연장하여 x축에 붙일 수 있습니다. 그러고 나면, L-모양 직각다각형은 밑변이 x축에 붙어 있고, 서로 인접한 두 개의 직사각형이 붙어 있는 형태임을 알 수 있습니다. 이렇게 정의를 하면 정점의 수가 4와 6인 경우를 모두 고려하게 됩니다. 

가장 넓은 L-모양 직각다각형을 찾기 위하여, 역으로 두 직사각형이 붙어 있는 x좌표 x<sub>0</sub>을 고정해 봅시다. x &le; x<sub>0</sub>인 영역과 x &ge; x<sub>0</sub>인 영역은 독립적이므로, 각각에 대해 가장 넓은 직사각형을 구한 뒤 넓이를 더하면 됩니다. 즉, x = x<sub>0</sub> 왼쪽/오른쪽 영역에서, x = x<sub>0</sub>에 붙어 있으면서 히스토그램에 들어 있는 가장 넓은 직사각형을 구하면 됩니다.

이렇게 접근했을 때 첫 번째로 당면하는 문제는 x<sub>0</sub>이 너무 많다는 것입니다. 다행히도, x<sub>0</sub>으로 가능한 값들은 입력으로 주어진 x좌표들뿐입니다. 이는 f(x<sub>0</sub>)을 윗 문단의 상황에서 가장 넓은 L-모양 직각다각형의 넓이로 둔다면, f가 구간별로 선형인 함수(piecewise linear function)이며(연속 함수는 아닙니다), 끊기는 지점들이 입력으로 주어진 x좌표들뿐임을 관찰함으로써 알 수 있습니다.

남은 것은 x = x<sub>0</sub> 왼쪽 영역에서, 오른쪽 변이 x = x<sub>0</sub>에 붙어 있으면서 히스토그램에 들어 있는 가장 넓은 직사각형의 넓이를 구하는 것입니다. 오른쪽 영역에서 구하는 것은 똑같이 할 수 있습니다. 문제 자체가 히스토그램에서 가장 넓은 직사각형을 구하는 상황과 굉장히 유사합니다. 이 문제는 스택을 활용해 해결할 수 있는 방법이 잘 알려져 있습니다. 이 방법을 "알고리즘 X"라고 부르겠습니다.

알고리즘 X는 히스토그램을 왼쪽에서부터 오른쪽으로 훑습니다. 각 x좌표를 고려하는 상황에서, 스택에는 (높이 h, 해당 높이 이상이 유지되는 가장 왼쪽 x좌표 x<sub>l</sub>)의 쌍들이 들어 있습니다. 이 때, 오른쪽 변이 x = x<sub>0</sub>인 가장 넓은 직사각형을 구하기 위해 할 수 있는 가장 쉬운 생각은 스택을 모두 순회해 보는 것입니다. 스택의 원소 (h, x<sub>l</sub>)에 대해, 넓이는 h(x<sub>0</sub> - x<sub>l</sub>)입니다. 하지만 모두 순회하는 것은 굉장히 느립니다.

그런데, 식의 꼴을 살펴보면 기울기가 h이고 y절편이 -hx<sub>l</sub>인 직선임을 알 수 있습니다. 즉, 우리가 원하는 것은 여러 개의 직선들이 있을 때, x = x<sub>0</sub>에서 최댓값을 구하는 것입니다. 컨벡스 헐 트릭(Convex Hull Trick)을 사용할 수 있을 것이라고 생각할 수 있습니다. 마침, 알고리즘 X를 생각해 보면 스택에 저장된 h는 아래에서 위로 갈수록 순증가하기 때문에, 직선의 기울기가 순증가할 때 사용할 수 있는 컨벡스 헐 트릭에도 알맞아 보입니다.

문제는, 알고리즘 X에서 스택의 원소가 빠지기도 한다는 것입니다. 컨벡스 헐 트릭에서 추가된 직선 l에 의해 삭제된 직선들이 있을텐데, 스택에서 원소가 제거되는 과정에서 이 삭제된 직선들이 다시 복구되어야 하는 경우가 발생할 수 있습니다. 이 점을 해결하기 위해 크게 세 가지 방법이 있습니다.
- 스택을 삭제된 데이터가 보존되는 형태(Persistent Stack)로 관리합니다. 다음의 글을 참고하시면 도움이 됩니다. [http://codeforces.com/blog/entry/51684](http://codeforces.com/blog/entry/51684){:target="_blank"}
- 구간에 직선을 추가하고(즉, 선분을 추가하는 것), 특정 x좌표에서의 최대 y좌표를 구하는 자료구조가 있습니다(Li Chao Segment Tree). 스택의 어떤 원소 (h, x<sub>l</sub>)이 x = x<sub>r</sub>에서 제거된다고 하면, 해당 자료구조에서 [x<sub>l</sub>, x<sub>r</sub>] 구간에 y = h(x - x<sub>l</sub>)을 추가합니다. 모든 직선이 추가된 이후, 각 x좌표에서의 최댓값을 구하면 됩니다.
- 이 작업은 구간 트리(Segment Tree)의 각 노드에 컨벡스 헐 트릭 구조를 저장해놓는 방식으로도 구현할 수 있습니다. 추가해야 할 직선들에 대한 정보를 미리 처리한 뒤, h에 대해 오름차순 정렬하여 순서대로 추가하면 됩니다.

## 곧 있을 코드 페스티벌 본선을 기대해주세요!

예선 참가자 중 우수한 성적을 거둔 64명이 본선에 진출하게 됩니다. 예선 순위표는 홈페이지([https://www.kakaocode.com](https://www.kakaocode.com){:target="_blank"})에 같이 공지할 예정이니 참고하시기 바랍니다. 본선 진출자들이 즐거운 경험을 가지고 돌아갈 수 있도록, 카카오에서 열심히 준비하고 있으니 많이 기대해주세요!