AI(인공지능) - artificial intelligence

##### [1. Uninformed Search - 20.02.20 CYS](#Uninformed-Search)
##### [3. Adversarial Search(적대적 탐색) - 20.02.20 LHJ](#adversarial-search)



## Search Strategy
탐색 전략이란 어떤 노드부터 탐색할 것인지 그 순서를 정하는 것.

대표적으로 네가지 기준으로 탐색 전략을 평가한다.

1. completeness : 만약 답이 존재한다고 한다면 매번 그 답을 찾아내는가.
2. time complexity : 동작 수행 시간
3. space complexity : 메모리 사용량
4. optimality : 찾은 답은 최적해(lost-cost solution)인가.


## Uniformed Search
탐색. 문제에서 정의한 것 이외의 추가적인 정보가 없을 때 사용하는 Search Strategy 이다.

이 전략이 할 수 있는 행위는 자식 노드(Successor)를 생성하거나 목표 도달 여부를 구별하는 것 밖에 없다.

1. Breadth-First Search

    Complete 만족, Optimal 만족

    시간복잡도 :
      depth를 d라고 하고, tree의 가지(branch)를 b 라고 한다.

      b + b^2 + b^3 + b^4 + ... + b^d = O(b^d)

2. Uniformed-Cost Search

    만일 모든 과정의 Cost가 동일하다면 BFS가 이상적이나, 일반적으로 그렇지 않다.
Uniform-cost Search는 lowest path cost g(n)까지의 노드 n까지 Expand한다. 
즉 현재 Frontier에서 확장되지 않은 노드 중에서 가장 비용이 적은 노드부터 선택해서 확장하는 것을 의미한다.
이를 위해서는 Frontier가 Path Cost에 따라 정렬된 Priority Queue로 구현이 되어야 한다.
가장 낮은 비용의 노드가 먼저 위치하게 한다.

    Complete 만족, Optimal 만족


    시간복잡도는 O(b^1+⌊C∗/ϵ⌋)=b^d+1
    
    깊이가 깊어질수록 메모리 공간이 많이 필요하다.

    
    <img src="./assets/UCS.png" width="70%" height="70%">
    
3. Depth-First Search

    Complete X, Optimal X
    현 트리구조의 최대깊이를 m이라고 노드의 개수는 오직 O(m)의 메모리만을 사용하면 된다.
    순환 고리가 없는 트리구조에서는 Complete를 만족한다.

    시간복잡도 : O(b^D)
    공간복잡도 : O(bD)

4. Depth-Limited Search

    무한한 State space에서의 Depth-first Search는 실패를 일으킬 수 있는데, 미리 설정해놓은 깊이 값인 l을 이용함으로써 이 실패를 줄일 수 있다. 즉, 깊이 l까지 도달하면 더 이상의 자식노드는 존재하지 않는다고 간주하는 알고리즘이다.
이 알고리즘의 Time-complexity는 O(bl)이 되며, Space-complexity는 O(bl)이 된다.

    
    <img src="./assets/DLS.png" width="70%" height="70%">

5. Iterative Deepening Depth-First Search

    Depth Limit Search에서 Limit을 점차적으로 늘려나가는 방식.
전체 상태공간의 지름을 알지 못할때 사용하면 좋다.
Time-complexity로는 O(bd)이다. 
    
    <img src="./assets/IDS.png" width="70%" height="70%">
    
    
 
#### Overall
   
    
   <img src="./assets/overall.png" width="70%" height="70%">

---

## Adversarial Search

### Adversarial Search(적대 탐색) 란?

- AI 프로그램(게임 프로그램)들은 탐색 알고리즘으로 **[Minimax algorithm](#1.-Minimax-algorithm(최대최소-방법)),** **[alpha-beta pruning](#2.-Alpha-Beta-Pruning(알파-베타-방법))** 등을 사용하는데, 이러한 알고리즘을 사용한 탐색을 적대 탐색이라고 한다.

- 적대 탐색에서는 두 명의 게임플레이어 중 한 명이 이기거나, 지거나 ,비길 때까지 번갈아 행동하는 것을 가정한다. 또, 사용가치가 서로 상반되기 때문에 한쪽이 점수를 얻으면, 한쪽은 잃게 된다. 이러한 특성이 적대적인 상황을 만든다.

- 게임이론 용어 :

  - Deterministic : 어떤 행동의 결과도 예측 가능하다. 즉, operation이 정확히 수행된다.
  
  - turn-taking : 두 플레이어의 행동이 번갈아서 일어난다. 즉, 동시에 작동하는 경우가 없다.
  
  - zero-sum game : 모든 이득의 총합이 항상 제로인 게임
  
  - perfect information : 현재 모든 게임 상태는 완전히 관찰 가능하다. 즉, optimal하게 선택 가능하다.

<br>

**적대 탐색 알고리즘 소개 전 해당 장에서 필요한 정보**

- 해당 장에서는 두 명의 플레이어를 MAX와 MIN으로 표현한다.

- [Tic-Tac-Toe(삼목게임)에 대한 게임 트리](#Game-Tree-for-Tic-Tac-Toe)를 예시로 사용한다.

- 게임트리의 대략적인 사이즈

  - b = branching factor(각 노드의 자식 노드 수)
  
  - d = search depth 라고 할 때, **O(b^d)**
  
  - 체스의 경우, b ~ 35 / d ~ 100 으로 엄청 큰 사이즈이기 때문에 이것을 다 탐색하기는 어렵다. 그래서 Game-playing은 **한정된 시간에 최적의 결정**을 내리는 것을 강조한다.
  
  -  주요 쟁점은 " 커다란 게임트리에서 어떻게 optimal move를 탐색할 것인가? " 이다. 이를 위해 적대 탐색 알고리즘이 사용된다.
  
<br>  

#### Game Tree for Tic Tac Toe

<br>

<img src="./assets/tic1.png" width="65%" height="65%">

### 적대 탐색 알고리즘 종류

#### 1. Minimax algorithm(최대최소 방법)

- 본인 차례에는 본인에게 제일 유리한 수, 상대방 차례에는 본인에게 제일 불리한 수가 선택하며, 다음 턴만이 아니라 그 이후까지 바라보며 탐색하는 과정이다.

- **MAX** 가 X 를 표시하고, **MIN** 은 0 를 표시하며, **MAX** 가 먼저 시작한다고 가정하자. 깊이 제한이 2 인 경우, 레벨 2 의 모든 노드가 생성될 때까지 너비우선 탐색을 수행한 다음, 이들 노드에 대하여 평가 함수를 적용한다. 상태 p에 대한 평가 함수 e(p) 가 다음과 같이 주어진다고 하자.

  ```
  if MAX가 이기는 상태 : e(p) = ∞
  
  if MIN이 이기는 상태 : e(p) = -∞
  
  if 결정이 나지 않은 상태 : e(p) = (MAX가 이길수 있는 경우의 수) - (MIN이 이길수 있는 경우의 수)
  ```

만약 상태가 다음과 같다면, 

<img src="./assets/minimax1.png" width="20%" height="20%">

e(p) = 6 - 4 = 2 가 될 것이다.

<br>

**START**

탐색의 첫번째 단계

<img src="./assets/minimax2.png" width="50%" height="50%">


위부터 e(p)의 값이 각 1, -2, -1이기 때문에 MAX는 e(p) = 1 을 선택하여 행동할 것이다.

<br>

<img src="./assets/minimax3.png" width="20%" height="20%">


MIN은 여기에 대해 위 그림과 같이 X의 왼편에 O를 표시했다고 하자.(MIN은 좋은 탐색 전략을 갖고 있지 않다고 볼 수 있다.)

그리고 다시 MAX가 탐색을 수행하고 아래와 같은 탐색트리가 만들어진다.

<br>

<img src="./assets/minimax4.png" width="70%" height="70%">


여기서 두 가지 최상의 선택이 가능하지만, 빨간표시의 행동을 선택했다고 하자. 그렇다면 MIN은 패배를 피하기 위해 아래와 같은 행동을 취할 것이다.

<br>

<img src="./assets/minimax5.png" width="20%" height="20%">


MAX는 탐색을 다시 수행하여 아래와 같은 트리를 생성한다. MAX는 이번에도 최상의 선택을 할 것이고, 이 선택이 MAX의 패배를 피할 수 있는 행동이라는 것을 알 수있다. 그리고 다음 차례에서 MIN은 패배했다는 것을 알 수있고 게임은 종료된다.

<br>

<img src="./assets/minimax6.png" width="70%" height="70%">


#### 2. Alpha-Beta Pruning(알파 베타 방법)

- 위에 설명한 Minimax algorithm의 경우 탐색트리 생성 과정과 상태 평가 과정이 완전히 분리되어 있다. 즉, 트리 생성이 완전히 끝난 후에야 상태 평가가 시작된다. 그래서 비효율적인 전략이라고 볼 수 있다.

- 이를 보완하기 위해 나온 방법이 Alpha-Beta Pruning으로 최종 결정에 영향이 없는 노드들은 가지치기를 해 시간을 줄이는 것이다.

<br>

**Example**

<img src="./assets/Alpha1.png" width="60%" height="60%">

<br>

위 그림을 예로 들어 설명해보자.

해당 그림은 노드 A와 A의 자식이 생성되고, B의 자식 노드 C까지 생성된 직후이다.

여기서 A의 평가값이 -1인데, 이 시점에서 시작 노드의 평가값은 -1 이상으로 제한된다.

왜냐하면 시작 노드는 MAX 차례이므로 최댓값을 탐색할 것이다. 근데 이미 A에서 평가값 -1을 받았으므로 그보다 작은 값을 선택할 수는 없다. 이 하한을 시작 노드의 **Alpha Value(알파값)** 라고 한다.

반대로 노드 B를 보면 노드 C의 평가값이 -1이기 때문에 노드 B의 평가값은 -1이하로 제한된다는 것을 확인할 수 있다. 왜냐하면 노드 B는 MIN 차례이므로 최솟값을 탐색할 것이다. 근데 노드 C에서 평가값 -1을 받았으므로 그보다 큰 값을 선택할 수 없다. 노드 B에 대한 이러한 상한을 **Beta Value(베타값)** 라고 한다.

즉,  

**MAX 노드의 알파값은 자식 노드의 평가값 중 현재까지 가장 큰 값이 된다.**

**MIN 노드의 베타값은 자식 노드의 평가값 중 현재까지 가장 작은 값이 된다.**



알파값보다 작거나 같은 베타값을 갖는 노드의 탐색을 중단하는 것을 **알파 절단(Alpha cut-off)** 라고 하고,

그 반대를 **베타 절단(Beta cut-off)** 라고 한다. 

그리고 이러한 과정을 수행해 가는 모든 과정을 일반적으로 **Alpha-Beta Pruning(알파 베타 방법)** 이라고 한다.


