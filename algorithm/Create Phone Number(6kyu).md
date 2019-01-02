- 문제

```
Write a function that accepts an array of 10 integers (between 0 and 9), that returns a string of those numbers in the form of a phone number.

Example:
createPhoneNumber([1, 2, 3, 4, 5, 6, 7, 8, 9, 0]) // => returns "(123) 456-7890"
The returned format must be correct in order to complete this challenge. 
Don't forget the space after the closing parentheses!
```





- 나의풀이

```
function createPhoneNumber(numbers){
  let a = "(" + numbers.splice(0, 3).join("") + ") ";
  let b = numbers.splice(0, 3).join("");
  let c = "-" + numbers.slice().join("");
  return a+b+c;
}
```



- 다른사람풀이

```
function createPhoneNumber(numbers){
  var format = "(xxx) xxx-xxxx";
  
  for(var i = 0; i < numbers.length; i++)
  {
    format = format.replace('x', numbers[i]);
  }
  
  return format;
}
```

와..replace를 이렇게 쓸줄이야..!!!

이런 풀이를 볼 수 있어서 너무 기쁘다!