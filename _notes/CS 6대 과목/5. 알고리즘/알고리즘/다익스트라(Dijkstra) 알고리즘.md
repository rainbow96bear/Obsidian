# 다익스트라 알고리즘 설명

시작점에서 도착점까지 최단 거리를 구하는 알고리즘  
각 노드 간 연결에는 가중치가 있어 DFS로 구하는 거리가 아닌 실제 거리를 따져서 최단 거리를 구하는 알고리즘

- [[우선순위 큐]]를 활용한다.

![[Pasted image 20231025204145.png]]

위와 같이 연결된 그래프에서 A에서 H로 가는 최단 거리를 구하는 과정으로 다익스트라를 설명하겠습니다.

A에 연결된 경로는 B, C, D이고 가중치는 각각 3, 1, 2입니다.
아직 확인하지 않은 지점까지의 거리는 2^30으로 표현하겠습니다.

<table style="border: 1px solid black; border-collapse: collapse;">
  <tr>
    <th style="border: 1px solid black; padding: 10px;">Queue</th>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 10px;">B, C, D</td>
  </tr>
</table>

<table style="border: 1px solid black; border-collapse: collapse;">
  <tr>
    <th align="center" style="border: 1px solid black; padding: 10px;">A</th>
    <th align="center" style="border: 1px solid black; padding: 10px;">B</th>
    <th align="center" style="border: 1px solid black; padding: 10px;">C</th>
    <th align="center" style="border: 1px solid black; padding: 10px;">D</th>
    <th align="center" style="border: 1px solid black; padding: 10px;">E</th>
    <th align="center" style="border: 1px solid black; padding: 10px;">F</th>
    <th align="center" style="border: 1px solid black; padding: 10px;">G</th>
    <th align="center" style="border: 1px solid black; padding: 10px;">H</th>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 10px;">0</td>
    <td style="border: 1px solid black; padding: 10px;">3</td>
    <td style="border: 1px solid black; padding: 10px;">1</td>
    <td style="border: 1px solid black; padding: 10px;">2</td>
    <td style="border: 1px solid black; padding: 10px;">2^30</td>
    <td style="border: 1px solid black; padding: 10px;">2^30</td>
    <td style="border: 1px solid black; padding: 10px;">2^30</td>
    <td style="border: 1px solid black; padding: 10px;">2^30</td>
  </tr>
</table>

Queue에는 B, C, D가 저장되고 각 거리를 확인해두었습니다.

우선 순위 Queue에 의하여 가중치가 가장 적은 C가 뽑혀서 연결된 경로를 확인합니다.

C에 연결된 경로는 E이고 가중치는 2입니다.
A에서 E까지의 길이는 C의 값과 C와 E의 가중치를 더한 값입니다.

<table style="border: 1px solid black; border-collapse: collapse;">
  <tr>
    <th style="border: 1px solid black; padding: 10px;">Queue</th>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 10px;">B, D, E</td>
  </tr>
</table>

<table style="border: 1px solid black; border-collapse: collapse;">
  <tr>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">A</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">B</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">C</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">D</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">E</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">F</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">G</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">H</th>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">0</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">3</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">1</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">2</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">3</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">2^30</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">2^30</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">2^30</td>
  </tr>
</table>

Queue에는 B, D, E가 저장되고 각 거리를 확인해두었습니다.

우선 순위 Queue에 의하여 가중치가 가장 적은 D가 뽑혀서 연결된 경로를 확인합니다.

D에 연결된 경로는 E, F이고 가중치는 3, 1입니다.
E의 경우 D에서 E로 가는 경우는 5의 결과가 나오지만 이미 3을 가지고 있기에 E는 더 작은 값인 3을 유지합니다.
F의 경우 A에서 F까지의 길이는 D의 값과 D와 F의 가중치를 더한 값입니다.

<table style="border: 1px solid black; border-collapse: collapse;">
  <tr>
    <th style="border: 1px solid black; padding: 10px;">Queue</th>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 10px;">B, E, F</td>
  </tr>
</table>

<table style="border: 1px solid black; border-collapse: collapse;">
  <tr>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">A</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">B</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">C</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">D</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">E</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">F</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">G</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">H</th>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">0</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">3</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">1</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">2</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">3</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">3</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">2^30</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">2^30</td>
  </tr>
</table>

위와 같은 방법으로 Queue를 순환하며 값을 기록하면 아래의 결과가 나옵니다.

<table style="border: 1px solid black; border-collapse: collapse;">
  <tr>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">A</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">B</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">C</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">D</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">E</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">F</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">G</th>
    <th style="border: 1px solid black; padding: 10px; text-align: center;">H</th>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">0</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">3</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">1</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">2</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">3</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">3</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">4</td>
    <td style="border: 1px solid black; padding: 10px; text-align: center;">4</td>
  </tr>
</table>

# 코드 예시 (Golang)

```go
type bus struct {
    to int
    cost int
}

func Process(link map[int][]bus, start, end, N int) int {
	queue := &MinHeap{}
	heap.Init(queue)
	heap.Push(queue, bus{start, 0})
	distance := make(map[int]int)
	for i:=1 ; i<=N ; i++ {
		distance[i] = 1000000000
	}
	distance[start] = 0
	for queue.Len() > 0 {
		now := heap.Pop(queue).(bus)
		if now.cost > distance[now.to] {
			continue
		}
		for i := 0; i < len(link[now.to]); i++ {
			nextNode := link[now.to][i]
			if distance[now.to] + nextNode.cost < distance[nextNode.to] {
				distance[nextNode.to] = min(distance[now.to] + nextNode.cost, distance[nextNode.to])
				heap.Push(queue, nextNode)
			}
		}
	}
	return distance[end]
}
```
