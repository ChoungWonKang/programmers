### 문제 링크

https://school.programmers.co.kr/learn/courses/30/lessons/178871

### **문제 설명**

얀에서는 매년 달리기 경주가 열립니다. 해설진들은 선수들이 자기 바로 앞의 선수를 추월할 때 추월한 선수의 이름을 부릅니다. 예를 들어 1등부터 3등까지 "mumu", "soe", "poe" 선수들이 순서대로 달리고 있을 때, 해설진이 "soe"선수를 불렀다면 2등인 "soe" 선수가 1등인 "mumu" 선수를 추월했다는 것입니다. 즉 "soe" 선수가 1등, "mumu" 선수가 2등으로 바뀝니다.

선수들의 이름이 1등부터 현재 등수 순서대로 담긴 문자열 배열 `players`와 해설진이 부른 이름을 담은 문자열 배열 `callings`가 매개변수로 주어질 때, 경주가 끝났을 때 선수들의 이름을 1등부터 등수 순서대로 배열에 담아 return 하는 solution 함수를 완성해주세요.

---

### 제한사항

- 5 ≤ `players`의 길이 ≤ 50,000
    - `players[i]`는 i번째 선수의 이름을 의미합니다.
    - `players`의 원소들은 알파벳 소문자로만 이루어져 있습니다.
    - `players`에는 중복된 값이 들어가 있지 않습니다.
    - 3 ≤ `players[i]`의 길이 ≤ 10
- 2 ≤ `callings`의 길이 ≤ 1,000,000
    - `callings`는 `players`의 원소들로만 이루어져 있습니다.
    - 경주 진행중 1등인 선수의 이름은 불리지 않습니다.

---

### 입출력 예

| players | callings | result |
| --- | --- | --- |
| ["mumu", "soe", "poe", "kai", "mine"] | ["kai", "kai", "mine", "mine"] | ["mumu", "kai", "mine", "soe", "poe"] |

---

### 입출력 예 설명

입출력 예 #1

4등인 "kai" 선수가 2번 추월하여 2등이 되고 앞서 3등, 2등인 "poe", "soe" 선수는 4등, 3등이 됩니다. 5등인 "mine" 선수가 2번 추월하여 4등, 3등인 "poe", "soe" 선수가 5등, 4등이 되고 경주가 끝납니다. 1등부터 배열에 담으면 ["mumu", "kai", "mine", "soe", "poe"]이 됩니다.

---

### 나의 풀이

```python
def solution(players, callings):
    result = players
    for i in range(len(callings)):
        for j in range(len(players)):
            if players[j] == callings[i] :
                players[j] = players[j-1]
                players[j-1] = callings[i]
    return result
```

for문을 일일이 경우의 수마다 설정되게 하니 성능 테스트에서 실패가 나왔다.

### 성능 요약

| 테스트 1 〉 | 통과 (0.01ms, 10.2MB) |
| --- | --- |
| 테스트 2 〉 | 통과 (0.01ms, 10.3MB) |
| 테스트 3 〉 | 통과 (0.32ms, 10.2MB) |
| 테스트 4 〉 | 통과 (10.81ms, 10.3MB) |
| 테스트 5 〉 | 통과 (165.44ms, 10.3MB) |
| 테스트 6 〉 | 통과 (748.92ms, 10.8MB) |
| 테스트 7 〉 | 실패 (시간 초과) |
| 테스트 8 〉 | 실패 (시간 초과) |
| 테스트 9 〉 | 실패 (시간 초과) |
| 테스트 10 〉 | 실패 (시간 초과) |
| 테스트 11 〉 | 실패 (시간 초과) |
| 테스트 12 〉 | 실패 (시간 초과) |
| 테스트 13 〉 | 실패 (시간 초과) |
| 테스트 14 〉 | 통과 (0.02ms, 10.2MB) |
| 테스트 15 〉 | 통과 (0.01ms, 10.2MB) |
| 테스트 16 〉 | 통과 (0.02ms, 10.1MB) |


### 채점 결과

정확성: 56.3
합계: 56.3 / 100.0

```python
def solution(players, callings):
    # 각 플레이어의 위치를 저장하는 dict 생성
    positions = {player: index for index, player in enumerate(players)}
    
    for call in callings:
        idx = positions[call]
        # 첫 번째 위치가 아닌 경우 위치를 교환
        if idx > 0:
            # dict에서 위치 업데이트
            positions[players[idx - 1]], positions[players[idx]] = idx, idx - 1
            # 리스트에서 플레이어 위치 교환
            players[idx], players[idx - 1] = players[idx - 1], players[idx]

    return players
```

코드를 이리저리 수정해봤지만, 시간 효율성을 지키기 위해서는 딕셔너리를 이용할 수 밖에 없었다.

players의 선수 이름을 키로, 선수의 인덱스를 값으로 저장해놓는다.
### 성능 요약

0.01ms, 10.1MB

### 채점 결과

정확성: 100.0
합계: 100.0 / 100.
