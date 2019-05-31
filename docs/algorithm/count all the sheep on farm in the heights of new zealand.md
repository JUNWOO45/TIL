7kyu

- 문제

```
Every week (Friday and Saturday night), the farmer and his son count amount of sheep returned to the yard of their farm.

They count sheep on Friday night, the same goes for Saturday (suppose that sheep returned on Friday are not feeding back on hills on Saturday).

As sheep are not coming in one flock, you will be given two arrays (one for each night) representing number of sheep as they were returning to the yard during the evenings (entries are positive ints, higher than zero).

Farmer and his son know the total amount of their sheep, you will be given this number as third parameter.

Your goal is to calculate the amount of sheep lost (not returned) to the farm after Saturday night counting.

Example 1: Input: {1, 2}, {3, 4}, 15 --> Output: 5

Example 2: Input: {3, 1, 2}, {4, 5}, 21 --> Output: 6

Good luck! :-)
```



- 나의풀이

```
function lostSheep(friday,saturday,total){
  //your code here
  var fridaySum = 0;
  var saturdaySum = 0;
  for(var element of friday){
    fridaySum += element;
  }
  for(var element of saturday){
    saturdaySum += element;
  }
  return total - fridaySum - saturdaySum;
}
```



- 다른사람풀이

```
function lostSheep(friday,saturday,total){
  return friday.concat(saturday).reduce((s,l)=>s-l,total)
}
```

friday와 saturday 배열을 concat으로 합쳤네.

그리고 그 합친 배열을 reduce로 빼버리네..

initialValue 는 total.

콜백의 첫번째 호출에서 첫번째 인수가 바로 이 initialValue, total이다.

total에서 firday.concat(saturday)의 element들을 하나씩 빼나가는거다.



```
const lostSheep = (f,s,n) => n - [...f,...s].reduce((a,b) => a + b,0)
```

마찬가지로 reduce를 사용.

reduce안에서 빼지말고 reduce로는 friday와 saturday의 합을 더하고, 바깥에서 total에서 뺌으로써 구한방법.





// 근본적으로 큰 차이는 없지만, 내장함수를 유연하게 사용할줄 알아야겠다. 이게 참 어렵네 ㅠㅠ