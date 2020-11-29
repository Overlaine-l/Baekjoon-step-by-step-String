# 백준 단계별로 풀어보기 - 문자열
[백준](https://www.acmicpc.net)의 단계별로 풀어보기 중 [문자열](https://www.acmicpc.net/step/7)의 몇몇 문제를 풀어본 곳입니다.  
코드에 등장하는 여러 함수들의 이름은 그때그때 생각나는대로 적었기에, 그 뜻이 덜 와닿을수도 있습니다.  
또한, 홈페이지에서 주어진 input의 형태와 코드에서 가정하는 input의 형태가 다를 수도 있습니다. 형태 변환은 어려운 문제가 아니고, 백준 단계별로 풀어보기에서 가정하는 input의 형태는 항상 동일하므로 이 부분은 엄밀하게 작성되지 않았을 수도 있습니다. 

# 1. [숫자의 합](https://www.acmicpc.net/problem/11720)
- 문제  
N개의 숫자가 공백 없이 쓰여있다. 이 숫자를 모두 합해서 출력하는 프로그램을 작성하시오.

- Code 
~~~
def linesum(array, N):    # array : given string, N : the number of integers
    string= str(array)
    if len(string) != N:
        return 'ERROR'
    sum=0
    for num in string:
        sum += int(num)
    return sum
~~~

- Explanation  
array로 표현되는 input string과 N이 같은지 비교해보고, 같으면 결과를 출력하는 간단한 예제입니다.  
입력의 형태가 str이기 때문에, 이를 정수로 변환하여 더하기 위해 int를 사용합니다.  

# 2. [문자열 반복](https://www.acmicpc.net/problem/2675)
- 문제  
문자열 S를 입력받은 후에, 각 문자를 R번 반복해 새 문자열 P를 만든 후 출력하는 프로그램을 작성하시오. 즉, 첫 번째 문자를 R번 반복하고, 두 번째 문자를 R번 반복하는 식으로 P를 만들면 된다. S에는 QR Code "alphanumeric" 문자만 들어있다.  

- Code  
~~~
def repeating(R, S):
    P = ''
    for letter in S:
        P += letter*R
    return print(P)
~~~

- Explanation
