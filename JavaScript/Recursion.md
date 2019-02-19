<h1>
    Recursion
</h1>

- 재귀란 함수가 자기 자신을 호출하는 것을 의미.

  ~~~
  const factorial = function(number) {
      let result = 1;
      for(let i = 1; i <= number; i++) {
          result *= i;
      }
      
      return result;
  };
  
  factorial(3);	//6
  factorial(4);	//24
  ~~~

  이러한 factorial code를 재귀를 사용하여 바꿔볼 수 있습니다.

  ~~~
  const factorial = function(number) {
      if(number > 0) {
          return number * factorial(number - 1);
      } else {
          return 1;
      }
  };
  
  factorial(3);	//6
  factorial(4);	//24
  ~~~

  이렇게, 처음 코드처럼 한번에 풀지않고, 재귀적으로 문제를 해결하는것은 "분할 정복 알고리즘"의 하나입니다.

  어떠한 문제를 작은 조각으로 쪼개어 푸는 것이죠.

  재귀를 사용하는 것은 컴퓨터에게는 많은 부담을 주지만, 가독성을 높혀줍니다.

  따라서 성능을 중시한다면 재귀를 사용하지않는 것이 좋습니다.

<h3>
    메모이제이션
</h3>

: 메모이제이션이란 프로그래밍을 할 때 반복되는 결과를 메모리에 저장해서 다음에 같은 결과가 나올 때 빨리 실행하는 코딩 기법을 의미합니다.

~~~
const factorial = (function(){
    let save = {};
    cosnt fact = function(number) {
        if(number > 0) {
            let saved = save[number - 1] || fact(number - 1);
            let result = number * saved;
            save[number] = result;
            
            return result;
        } else {
            return 1;
        }
    }
    
    return fact;
})();
~~~

~~~
const fibonacci = function(number) {
    if(number < 2) {
        return number;
    } else {
        return fibonacci(number - 1) + fibonacci(number - 2);l
    }
};
~~~

이걸 factorial처럼 클로저를 사용해서 메모이제이션 해보면,

~~~
const fibonacci = (function() {
    let save = {};
    const fibo = function(number) {
        if(number < 2) {
            return number;
        } else {
            const saved1 = save[number - 1] || fibo(number - 1);
            const saved2 = save[number - 2] || fibo(number - 2);
            const result = saved1 + saved2;
            
            return result;
        }
    };
    
    return fibo;
})();

~~~

