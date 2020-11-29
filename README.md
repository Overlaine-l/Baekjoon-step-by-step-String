# 백준 단계별로 풀어보기 - 문자열
[백준](https://www.acmicpc.net)의 단계별로 풀어보기 중 [문자열](https://www.acmicpc.net/step/7)의 몇몇 문제를 풀어본 곳입니다.  
코드에 등장하는 여러 함수들의 이름은 그때그때 생각나는대로 적었기에, 그 뜻이 덜 와닿을수도 있습니다.  
또한, 홈페이지에서 주어진 input의 형태와 코드에서 가정하는 input의 형태가 다를 수도 있습니다. 형태 변환은 어려운 문제가 아니고, 백준 단계별로 풀어보기에서 가정하는 input의 형태는 항상 동일하므로 이 부분은 엄밀하게 작성되지 않았을 수도 있습니다.  
모든 코드는 배워가는 입장에서 작성한 만큼, 더 좋은 방법이 있을 수 있습니다.

## 1. 숫자의 합
- [문제](https://www.acmicpc.net/problem/11720)  
N개의 숫자가 공백 없이 쓰여있다. 이 숫자를 모두 합해서 출력하는 프로그램을 작성하시오.

- 코드 
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

- 설명  
array로 표현되는 input string과 N이 같은지 비교해보고, 같으면 결과를 출력하는 간단한 예제입니다.  
입력의 형태가 str이기 때문에, 이를 정수로 변환하여 더하기 위해 int를 사용합니다.  
참고로, 위의 'input string과 N이 같은지 비교해보'는 과정은 이후 문제에서는 생략되는 경우가 많습니다. 이는 다른 이유가 아니고, 굳이 만들 필요가 없어서 그렇습니다. 만약 해당 검증 코드가 필요하다면 반드시 만들어야 합니다만, 단계별로 풀어보기의 거의 모든 문제에서 같은 방법으로 검증 코드를 만들 수 있스므로 앞으로의 풀이에서는 생략될 것입니다.  

## 2. 문자열 반복
- [문제](https://www.acmicpc.net/problem/2675)  
문자열 S를 입력받은 후에, 각 문자를 R번 반복해 새 문자열 P를 만든 후 출력하는 프로그램을 작성하시오. 즉, 첫 번째 문자를 R번 반복하고, 두 번째 문자를 R번 반복하는 식으로 P를 만들면 된다. S에는 QR Code "alphanumeric" 문자만 들어있다.  

- 코드  
~~~
def repeating(R, S):
    P = ''
    for letter in S:
        P += letter*R
    return print(P)
~~~

- 설명  
각 문자마다 R번 반복해서 더하기 위해 for로 각 문자를 추출해 \*로 반복 횟수를 지정합니다.  
문자열에 곱하기(\*)를 하면 반복된다는 점은 어렵지 않는 내용입니다.  

## 3. 단어 공부
- [문제](https://www.acmicpc.net/problem/1157)  
알파벳 대소문자로 된 단어가 주어지면, 이 단어에서 가장 많이 사용된 알파벳이 무엇인지 알아내는 프로그램을 작성하시오. 단, 대문자와 소문자를 구분하지 않는다.  

- 코드  
~~~
import operator
def maxused(S):
    S=S.upper()
    collect={}
    appeared = []
    
    for letter in S:
        if letter in appeared :
            collect[letter]+=1
        else:
            appeared.append(letter)
            collect[letter]=1
            
    a = max(collect)
    ans = max(collect.items(), key=operator.itemgetter(1))[0]
    
    collect.pop(max(collect.items(), key=operator.itemgetter(1))[0])
    if max(collect) == a:
        return '?'
    else:
        return ans
~~~

- 설명  
우선, 대소문자를 구분하지 않으므로 (예시 입/출력에 나와있듯) 대문자로 된 출력을 만들기 위해 주어진 문자열 S의 모든 알파벳을 upper 명령어를 이용해 대문자로 만듭니다. 물론 소문자로 만들고 다시 대문자로 바꿔도 상관없지만 굳이 그럴 필요는 없겠죠?  
다음으로, 이 문제에서 데이터들을 저장할 때 사용할 자료형은 다음 2가지입니다.  
1. **collect**(dictionary 자료형) : 입력된 string에서 사용된 문자(A~Z)를 key로, 사용된 횟수를 value로 가집니다.  
2. **appeared**(list 자료형) : 사용된 문자들을 저장합니다. 입력 string의 각 문자들이 이미 나온 문자인지를 판별할 때, appear 안에 있는지를 확인하는 방식으로 판별하기 위해 존재합니다.  
그 후 나오는 for문은, 사용된 문자들을 셉니다.  
가장 많이 사용된 문자 중 하나와 그 횟수를 각각 ans와 a에 지정합니다. 이 때, max는 dictionary의 value를 출력하는 반면에 우리가 필요한 결과는 key이므로, value를 구한 후 operator를 이용해 해당 value를 가지는 key를 뽑아냅니다.  
이 때, key가 하나 이상 있을 수 있기에 pop을 이용해 방금 나온 ans : a를 dictionary에서 빼내고 다음으로 가장 많이 나온 알파벳을 (동일한 방법으로) 출력합니다. 만약 두 값이 같으면 ?를, 그렇지 않다면 처음 뽑은 ans가 출력되도록 if를 이용해 출력 부분 코드를 짭니다.  

## 4. 그룹 단어 체커

- [문제](https://www.acmicpc.net/problem/1316)  
그룹 단어란 단어에 존재하는 모든 문자에 대해서, 각 문자가 연속해서 나타나는 경우만을 말한다. 예를 들면, ccazzzzbb는 c, a, z, b가 모두 연속해서 나타나고, kin도 k, i, n이 연속해서 나타나기 때문에 그룹 단어이지만, aabbbccb는 b가 떨어져서 나타나기 때문에 그룹 단어가 아니다.  
단어 N개를 입력으로 받아 그룹 단어의 개수를 출력하는 프로그램을 작성하시오.  

- 코드  
~~~
def groupped_word():
    raw = input().split('\n')
    N = int(raw.pop(0))
    
    if N != len(raw):
        return 'ERROR'
    
    def checker(word):
        prev_word = word[0]
        word_list = [word[0]]
        for e in word[1:]:
            if e not in word_list:
                word_list.append(e)
            elif e in word_list and e != prev_word:
                return 0
            prev_word = e
        return 1
    
    ans = 0
    for word in raw:
        ans += checker(word)
        
    return ans
~~~

- 설명  
이 코드의 앞부분은, 문제 원본에 있는 입력을 그대로 넣었을 때 사용하기 편한 방식으로 가공하는 법을 다루고 있습니다. 이후에는 이러한 처리를 이용하는 경우가 점점 많아질 겁니다.  
문제를 보면 알 수 있듯, 문제에서 가정하는 입력은 숫자 혹은 문자들로 이루어진 multiline이고, 각 line에서 주어지는 input은 비슷한 형태을 가집니다. 그렇기에, multiline input을 line별로 쪼개는 것이 우선입니다.  
input()은 함수 groupped_word()를 실행시킨 후 input을 입력할 수 있도록 해줍니다. 이 multiline input을 line별로 쪼개기 위해 input().split('\n')을 사용합니다. split 함수의 괄호 안에 있는 문자는 쪼개는 경계선이 되는 문자이며, 여기서는 line별로 쪼개기 위해 enter(줄 바꾸기)를 의미하는 '\n'을 괄호 안에 넣었습니다. 참고로 input 함수는 받은 입력을 string으로 간주하기 때문에, \n이 아닌 '\n'으로 써야 합니다.  
입력에서 처음 주어지는, 문자의 개수와 실제 입력으로 들어온 문자의 개수가 같은지 판별하기 위해 if문이 등장합니다. 꼭 필요한 내용은 아닙니다.  
다음으로 주어지는 내부 함수는, 각 단어가 주어진 조건을 만족하는지 체크합니다. 각 단어가 조건을 만족하려면 단어의 모든 알파벳 e에 대해서 다음 두 조건 중 하나가 성립해야 합니다:  
1. e는 이전에 등장한 적이 없다.  
2. e와, e 바로 앞에 등장한 알파벳은 같은 알파벳이다.  
첫 번째를 체크하기 위해 이전에 등장했던 단어들을 모아놓는 word_list(list 자료형)가, 두 번째를 체크하기 위해 이전 단어를 의미하는 prev_word(str 자료형)가 등장합니다. word_list는 새로운 알파벳이 나올 때마다 추가하면 그만이지만, prev_word는 그 알파벳이 계속 바뀌어야 하므로 for문의 가장 마지막에 prev_word = e를 통해 설정해줍니다.  
만약 두 조건이 모두 만족이 안되는 경우(elif문), 함수가 즉시 중단되고 조건을 만족하지 않는다는 의미인 0이 출력됩니다. 모든 e에 대해 조건이 만족되면 1이 출력됩니다.  
마지막으로, 출력을 위와 같이 지정했기 때문에 입력의 각 line에 있는 word의 출력값을 다 더하면, 원하는 전체 출력값이 나옵니다.
