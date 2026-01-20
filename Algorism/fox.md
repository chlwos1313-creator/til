# [String] 문자열에서 'fox' 제거하기 (Stack 활용)

## 1. 문제 개요
- **문제:** 주어진 문자열에서 "fox"라는 단어를 모두 찾아 제거한다.
- **조건:** "fox"를 제거한 뒤, 남은 문자들이 합쳐져서 또 "fox"가 되면 그것도 제거해야 한다. (예: `ffoxox` -> 가운데 `fox` 삭제 -> 남은 `fox` 삭제 -> 빈 문자열)
- **유형:** 자료구조 (Stack), 문자열 처리

## 2. 접근 방법 (Why Stack?)
처음에는 파이썬의 `replace()` 함수를 반복문(`while`)으로 돌려서 풀려고 했다.
하지만 문자열 길이가 길어지면 `replace`는 매번 문자열을 새로 만들기 때문에 **시간 초과(Time Limit)**가 날 위험이 있다.

따라서 **스택(Stack)**을 사용하여 한 번만 훑으면서(`O(N)`) 처리하는 것이 효율적이다.

## 3. 코드 구현 (Python)

```python
def solve(text):
    stack = []
    target = list("fox") # ['f', 'o', 'x']
    
    for char in text:
        stack.append(char)
        
        # 스택의 끝부분 3글자가 ['f', 'o', 'x'] 인지 확인
        if len(stack) >= 3 and stack[-3:] == target:
            # 맞다면 3번 pop하여 제거 (fox 날리기)
            for _ in range(3):
                stack.pop()
                
    return "".join(stack)

# 테스트
input_str = "ffoxox"
print(solve(input_str))  # 결과: "" (빈 문자열)