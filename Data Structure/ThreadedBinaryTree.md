# 스레드 이진 트리(Threaded binary tree)

이진 트리의 한 종류로 가리키는 곳이 없는 모든 오른쪽 널 포인터(null pointer)를 중위 후속자 노드로 연결하고, 가리키는 곳이 없는 모든 왼쪽 널 포인터를 중위 선행자 노드로 연결한 것이다.

- 재귀적인 중위 순회를 빠르게 할 수 있는 방법이다.
- 부모 포인터나 스택을 사용하지 않고도 노드의 부모를 찾을 수 있게 해준다.
    - 스택 공간을 쓸 수 없거나, 부모 노드의 위치를 알 수 없을 때 유용하게 사용될 수 있다.

✔️중위 순회

- 이진 탐색 트리에서 사용되는 트리이다.
- 왼쪽 서브 트리를 중위 순회한다. 노드를 방문한다. 오른쪽 서브 트리를 중위 순회한다.
- <img src="./imgs/binary_tree.png" width="40%" height="30%">
- 이진 탐색 트리 중위 순회: A, B, C, D, E, F, G, H, I (left, root, right)
- 이진 탐색 트리의 구현은 트리의 높이에 비례한 호출 스택 공간이 필요하다.

### 스레드 이진 트리란?

<img src="./imgs/threaded-binary-tree.png" width="60%" height="30%">

<일반적인 이진 트리>

- 이진 트리의 연결 표현에서 링크 필드의 절반 이상이 null 값을 포함하므로 저장 공간이 낭비 된다.
    - 이진 트리가 n개의 노드로 구성된 n+1개의 링크 필드에는 null 값이 포함된다.
    - 스레드 이진 트리는 이를 효율적으로 사용하기 위해 null 링크를 스레드로 대체한다.
- 스레드 이진 트리의 각 노드에는 자식 노드에 대한 링크나 트리의 다른 노드에 대한 스레드가 포함되어 있다.

<img src="./imgs/threadedbinarytree.png" width="60%" height="40%">

<스레드 이진 트리>

---

참고

[Threaded Binary Tree - javatpoint](https://www.javatpoint.com/threaded-binary-tree)
