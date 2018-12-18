- 문제내용

```
Your task
Given a dictionary/hash/object of languages and your respective test results, return the list of languages where your test score is at least 60, in descending order of the results.

Note: There will be no duplicate values.

Examples
{"Java": 10, "Ruby": 80, "Python": 65}  --> ["Ruby", "Python"]
{"Hindi": 60, "Dutch" : 93, "Greek": 71} --> ["Dutch", "Greek", "Hindi"]
{"C++": 50, "ASM": 10, "Haskell": 20}   --> []
My other katas
If you enjoyed this kata then please try my other katas! :-)

Translations are welcome!
```



- clever solution

```
function myLanguages(results) {
  return Object.keys(results).filter(function(r) {
    return results[r] >= 60;
  }).sort(function(a, b) {
    return results[b] - results[a];
  });
}
```

메소드를 자유자재로 다루어야 이렇게 깔끔한 답이 나올것같습니다.

results의 key값들을 뽑아내고, results[key]들이 조건을 만족하고, 또한 그 만족한것들을 sort로 정렬하고..

쉬운문제임에도 돌아가고, 막히는 점을 얼른 고쳐야겠습니다.