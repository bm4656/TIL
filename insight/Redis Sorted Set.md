### ✅ Sorted Set

- 순위표/랭킹 구현에 사용
- 특정인의 순위 알 수 있음

### ✅ Skip List

Sorted Set 구현에 사용한 자료 구조는 Skip List

![Redis_Sorted_Set_1.png](../.images/Redis_Sorted_Set_1.png)

- 연결 리스트가 계층을 구성함 → 0, 1, 2 레벨
- 각 연결 리스트는 값을 순서대로 가짐
- 0 레벨: 전체 값을 가짐
- 상위 레벨: 하위 노드에서 일부 노드만 포함

**검색 - 30 찾기**
- 만약 0레벨처럼 단일 연결 리스트 구조라면 앞에서부터 순차적으로 검색할 것이다.

![Redis_Sorted_Set_2.png](../.images/Redis_Sorted_Set_2.png)

- 계층 구조를 가지고 있는 Skip List는 가장 최상위 레벨에서부터 시작한다.

```tsx
- 2레벨 HEAD 노드에서 다음노드 확인 → 40, 30보다 크군 더이상 진행 X, 한 칸 내려감

- 1레벨 HEAD 노드에서 다음노드 확인 → 20, 30보다 작군, 다음노드 확인 → 40, 30보다 크군 더이상 진행 X, 한 칸 내려감

- 0레벨 20노드에서 다음노드 확인 → 30이 있네!
```

- 삽입과 삭제도 비슷한 방식으로 자리를 찾아간다.
- 평균 O(log n)의 시간복잡도를 가진다.

**값 70의 랭킹은?**

![Redis_Sorted_Set_3.png](../.images/Redis_Sorted_Set_3.png)

- 그냥 0레벨에서 순서대로 찾으면 O(n)
- Skip List에서는 랭킹을 찾기 위해서 새로운 정보를 하나 추가한다.

![Redis_Sorted_Set_4.png](../.images/Redis_Sorted_Set_4.png)

- **각 노드간의 간격(칸)을 추가한다. → SPAN**

![Redis_Sorted_Set_5.png](../.images/Redis_Sorted_Set_5.png)

- 동일하게 최상위 레벨부터 시작한다.
- 이런식으로 O(log n)의 시간복잡도로 랭킹을 구할 수 있다.

**키 c의 랭킹은?**

![Redis_Sorted_Set_6.png](../.images/Redis_Sorted_Set_6.png)

- 해시테이블로 (키, 값) 쌍을 유지
- 먼저 c에 해당하는 값을 구하고, 랭킹을 찾아간다.

### ✅ **정리**

**Redis Sorted Set = Skip List + Hashtable**

- 랭킹을 구하기 위해 내부적으로 부가정보인 SPAN 값을 관리한다.
- 단점 → 계층 구조에 따른 메모리 사용량 증가

[🔗 출처 링크](https://www.youtube.com/watch?v=-titFXvd5xE)