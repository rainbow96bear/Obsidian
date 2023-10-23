A를 B번 거듭 제곱하는 알고리즘

시간 복잡도 - N
answer := 1
for i:=0 ; i<B ; i++ {
	answer * = A
}
가장 기본적인 거듭제곱 형태

시간 복잡도 - O(logN)
A^B에서 B를 2진법으로 표현하여 생각

예를 들어 B가 13인 경우 0b1101이고
A^8 * A^4 * A^1로 풀어서 표현이 가능하다.

answer := 1
for B>0 {
	if B%2 == 1 {
		answer * = A
	}
	A * = A
}
