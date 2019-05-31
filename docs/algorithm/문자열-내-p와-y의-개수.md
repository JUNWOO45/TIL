```
나의 풀이

function solution(s){
    var countP = 0;
    var countY = 0;
    
    for(var i = 0; i < s.length; i++){
        if(s[i] === 'p' || s[i] === 'P'){
            countP++
        } else if (s[i] === 'y' || s[i] === 'Y') {
            countY++
        }
    }
    if(countP === countY){
        return true;
    } else if(countP === 0 && countY === 0){
        return true;
    } else {
        return false;
    }
}
```

```
다른 사람의 풀이
function numPY(s){
    return s.toUpperCase().split("P").length === s.toUpperCase().split("Y").length;
}
//엄청 깔끔하네.... 와우..
```









