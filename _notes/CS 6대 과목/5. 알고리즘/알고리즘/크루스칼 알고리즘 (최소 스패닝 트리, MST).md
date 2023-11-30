# **최소 스패닝 트리 (MST)**

최소 스패닝 트리는 주어진 연결된 그래프에서 모든 정점을 포함하면서 그래프의 모든 정점을 연결하는 간선의 부분 집합 중에서 가중치의 합이 최소인 트리를 말합니다.

최소 스패닝 트리를 찾는 알고리즘은 크게 두 가지가 있습니다. 그중 크루스칼 알고리즘에 대하여 알아보겠습니다.

<img src="/assets/스크린샷 2023-11-30 110856.png">

위와 같이 연결된 그래프에서 크루스칼 알고리즘을 통하여 MST를 구하는 방법을 알아보겠습니다.

각 Node와 연결되는 간선의 정보를 배열에 저장합니다. ex) Edge {A, B, 1}

각 Node의 부모 노드를 판별하기 위한 Parent 배열을 생성합니다. (Node의 알파벳을 각 번호로 변)

초기 값은 자기 자신을 부모로 지정합니다.

크루스칼 알고리즘을 통한 최소 경로를 가지는 트리를 확인하는 방법은 간선의 가중치가 가장 낮은 간선을 먼저 확인하는 것입니다.

간선 정보를 저장한 배열을 가중치를 기준으로 정렬을 합니다.

정렬 후 totalWeight를 찾는 과정은 아래와 같습니다.

각 노드의 부모 값을 확인하고 서로의 부모가 다르다면 부모 값을 통일하여 연결되어 있다는 것을 기록하고 totalWeight를 증가시킵니다.

```
for i:=0 ; i <len(EdgeList) ; i++ {
    fromRoot := FindRoot(EdgeList[i].from, Parent)
    toRoot := FindRoot(EdgeList[i].to, Parent)

    if fromRoot != toRoot {
        Parent[fromRoot] = toRoot
        totalWeight += EdgeList[i].value
    }
}
```

**EdgeList**
<table style="border-collapse: collapse; width: 100%; height: 34px;" border="1" data-ke-align="alignLeft" data-ke-style="style8">
<tbody>
<tr style="height: 17px;">
<td style="width: 10%; height: 17px; text-align: center;">A,B</td>
<td style="width: 10%; height: 17px; text-align: center;">E,G</td>
<td style="width: 10%; height: 17px; text-align: center;">B,C</td>
<td style="width: 10%; height: 17px; text-align: center;">E,F</td>
<td style="width: 10%; height: 17px; text-align: center;">B,D</td>
<td style="width: 10%; height: 17px; text-align: center;">C,F</td>
<td style="width: 10%; height: 17px; text-align: center;">G,H</td>
<td style="width: 10%; height: 17px; text-align: center;">C,E</td>
<td style="width: 10%; height: 17px; text-align: center;">F,H</td>
<td style="width: 10%; height: 17px; text-align: center;">D,E</td>
</tr>
<tr style="height: 17px;">
<td style="width: 10%; height: 17px; text-align: center;">1</td>
<td style="width: 10%; height: 17px; text-align: center;">1</td>
<td style="width: 10%; height: 17px; text-align: center;">2</td>
<td style="width: 10%; height: 17px; text-align: center;">2</td>
<td style="width: 10%; height: 17px; text-align: center;">3</td>
<td style="width: 10%; height: 17px; text-align: center;">3</td>
<td style="width: 10%; height: 17px; text-align: center;">3</td>
<td style="width: 10%; height: 17px; text-align: center;">4</td>
<td style="width: 10%; height: 17px; text-align: center;">5</td>
<td style="width: 10%; height: 17px; text-align: center;">6</td>
</tr>
</tbody>
</table>
**Parent**
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 12.5%; text-align: center;">A(1)</td>
<td style="width: 12.5%; text-align: center;">B(2)</td>
<td style="width: 12.5%; text-align: center;">C(3)</td>
<td style="width: 12.5%; text-align: center;">D(4)</td>
<td style="width: 12.5%; text-align: center;">E(5)</td>
<td style="width: 12.5%; text-align: center;">F(6)</td>
<td style="width: 12.5%; text-align: center;">G(7)</td>
<td style="width: 12.5%; text-align: center;">H(8)</td>
</tr>
<tr>
<td style="width: 12.5%; text-align: center;">1</td>
<td style="width: 12.5%; text-align: center;">2</td>
<td style="width: 12.5%; text-align: center;">3</td>
<td style="width: 12.5%; text-align: center;">4</td>
<td style="width: 12.5%; text-align: center;">5</td>
<td style="width: 12.5%; text-align: center;">6</td>
<td style="width: 12.5%; text-align: center;">7</td>
<td style="width: 12.5%; text-align: center;">8</td>
</tr>
</tbody>
</table>
---

Edge의 첫 번째 값을 확인하여 두 Node의 부모를 확인 후 다르다면 A의 Parent를 B의 Parent로 변경합니다.

간선의 값만큼 전체 가중치를 증가시킨다.

<img src="/assets/스크린샷 2023-11-30 113915.png">
**totalValue** \= 1

**Parent**
<table style="border-collapse: collapse; width: 100%; height: 34px;" border="1" data-ke-align="alignLeft">
<tbody>
<tr style="height: 17px;">
<td style="width: 12.5%; height: 17px; text-align: center;">A(1)</td>
<td style="width: 12.5%; height: 17px; text-align: center;">B(2)</td>
<td style="width: 12.5%; height: 17px; text-align: center;">C(3)</td>
<td style="width: 12.5%; height: 17px; text-align: center;">D(4)</td>
<td style="width: 12.5%; height: 17px; text-align: center;">E(5)</td>
<td style="width: 12.5%; height: 17px; text-align: center;">F(6)</td>
<td style="width: 12.5%; height: 17px; text-align: center;">G(7)</td>
<td style="width: 12.5%; height: 17px; text-align: center;">H(8)</td>
</tr>
<tr style="height: 17px;">
<td style="width: 12.5%; height: 17px; text-align: center;">2</td>
<td style="width: 12.5%; height: 17px; text-align: center;">2</td>
<td style="width: 12.5%; height: 17px; text-align: center;">3</td>
<td style="width: 12.5%; height: 17px; text-align: center;">4</td>
<td style="width: 12.5%; height: 17px; text-align: center;">5</td>
<td style="width: 12.5%; height: 17px; text-align: center;">6</td>
<td style="width: 12.5%; height: 17px; text-align: center;">7</td>
<td style="width: 12.5%; height: 17px; text-align: center;">8</td>
</tr>
</tbody>
</table>
---

다음 Edge의 값을 확인하여 E와 G Node를 대상으로 동일한 작업을 진행합니다.

<img src="/assets/스크린샷 2023-11-30 114056.png">
**totalValue** \= 2

**Parent**
<table style="border-collapse: collapse; width: 100%; height: 34px;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="text-align: center;">A(1)</td>
<td style="text-align: center;">B(2)</td>
<td style="text-align: center;">C(3)</td>
<td style="text-align: center;">D(4)</td>
<td style="text-align: center;">E(5)</td>
<td style="text-align: center;">F(6)</td>
<td style="text-align: center;">G(7)</td>
<td style="text-align: center;">H(8)</td>
</tr>
<tr>
<td style="text-align: center;">2</td>
<td style="text-align: center;">2</td>
<td style="text-align: center;">3</td>
<td style="text-align: center;">4</td>
<td style="text-align: center;">7</td>
<td style="text-align: center;">6</td>
<td style="text-align: center;">7</td>
<td style="text-align: center;">8</td>
</tr>
</tbody>
</table>
---

B와 C도 같은 작업을 한 후 E와 F를 확인해 보면 E의 부모는 G이고 F의 부모는 F이므로 값이 다르기에 E의 부모의 부모 즉 G의 부모를 F로 지정합니다.

<img src="/assets/스크린샷 2023-11-30 115601.png">
**totalValue** \= 6

**Parent**
<table style="border-collapse: collapse; width: 100%; height: 34px;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="text-align: center;">A(1)</td>
<td style="text-align: center;">B(2)</td>
<td style="text-align: center;">C(3)</td>
<td style="text-align: center;">D(4)</td>
<td style="text-align: center;">E(5)</td>
<td style="text-align: center;">F(6)</td>
<td style="text-align: center;">G(7)</td>
<td style="text-align: center;">H(8)</td>
</tr>
<tr>
<td style="text-align: center;">2</td>
<td style="text-align: center;">3</td>
<td style="text-align: center;">3</td>
<td style="text-align: center;">4</td>
<td style="text-align: center;">7</td>
<td style="text-align: center;">6</td>
<td style="text-align: center;">6</td>
<td style="text-align: center;">8</td>
</tr>
</tbody>
</table>
---

이러한 과정이 반복되면 최종적으로 연결된 간선과 Parent의 값은 아래와 같습니다.

<img src="/assets/스크린샷 2023-11-30 115835.png">
**totalValue** \= 15

**Parent**
<table style="border-collapse: collapse; width: 100%; height: 34px;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="text-align: center;">A(1)</td>
<td style="text-align: center;">B(2)</td>
<td style="text-align: center;">C(3)</td>
<td style="text-align: center;">D(4)</td>
<td style="text-align: center;">E(5)</td>
<td style="text-align: center;">F(6)</td>
<td style="text-align: center;">G(7)</td>
<td style="text-align: center;">H(8)</td>
</tr>
<tr>
<td style="text-align: center;">2</td>
<td style="text-align: center;">3</td>
<td style="text-align: center;">4</td>
<td style="text-align: center;">6</td>
<td style="text-align: center;">7</td>
<td style="text-align: center;">6</td>
<td style="text-align: center;">6</td>
<td style="text-align: center;">6</td>
</tr>
</tbody>
</table>
---

위의 상황에서 연결되지 않은 간선의 경우 연결을 시도하게 되면 부모의 값이 동일하다는 결과가 나옵니다.

C의 최 상위 부모 : F(6) C->D->F

E의 최 상위 부모 : F(6) E->G->F

위의 방법을 통하여 MST를 구할 수 있었습니다.

# **핵심 코드**

**간선 연결 Process**

```
func Process(V int, EdgeList []Edge) int {

	Parent := make([]int, V+1)
	for i:=1 ; i<=V ; i++ {
		Parent[i]=i
	}
	sort.Slice(EdgeList, func(i, j int)bool {return EdgeList[i].value < EdgeList[j].value})
	
	var totalWeight int

	for i:=0 ; i <len(EdgeList) ; i++ {
		fromRoot := FindRoot(EdgeList[i].from, Parent)
		toRoot := FindRoot(EdgeList[i].to, Parent)

		if fromRoot != toRoot {
			Parent[fromRoot] = toRoot
			totalWeight += EdgeList[i].value
		}
	}
	return totalWeight
}
```

**FindRoot**

```
func FindRoot(num int, Parent []int) int {
	if Parent[num] == num {
		return Parent[num]
	}
	Parent[num] = FindRoot(Parent[num], Parent)
	return Parent[num]
}
```