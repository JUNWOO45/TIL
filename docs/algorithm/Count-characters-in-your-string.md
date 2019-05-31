6kyu



- 문제

```
The main idea is to count all the occuring characters(UTF-8) in string. If you have string like this aba then the result should be { 'a': 2, 'b': 1 }

What if the string is empty ? Then the result should be empty object literal { }
```



- 나의풀이

```
function count (string) {  
  // The function code should be here
  if(string === ""){
    return {}; 
  }
  var splitted = string.split('');
  var container = {};
  
  for(let i = 0; i < splitted.length; i++){
    var check = Object.keys(container);
    if(check.includes(splitted[i])){
      container[splitted[i]]++
    } else {
      container[splitted[i]] = 1;
    }
  }
  return container;
}
```



- 다른사람풀이

```
function count (string) {  
  var count = {};
  string.split('').forEach(function(s) {
     count[s] ? count[s]++ : count[s] = 1;
  });
  return count;
}
```

깰끔.......