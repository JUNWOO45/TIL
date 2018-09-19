codewars

- 문제

```
In a small town the population is p0 = 1000 at the beginning of a year. The population regularly increases by 2 percent per year and moreover 50 new inhabitants per year come to live in the town. How many years does the town need to see its population greater or equal to p = 1200 inhabitants?

At the end of the first year there will be: 
1000 + 1000 * 0.02 + 50 => 1070 inhabitants

At the end of the 2nd year there will be: 
1070 + 1070 * 0.02 + 50 => 1141 inhabitants (number of inhabitants is an integer)

At the end of the 3rd year there will be:
1141 + 1141 * 0.02 + 50 => 1213

It will need 3 entire years.
More generally given parameters:

p0, percent, aug (inhabitants coming or leaving each year), p (population to surpass)

the function nb_year should return n number of entire years needed to get a population greater or equal to p.

aug is an integer, percent a positive or null number, p0 and p are positive integers (> 0)

Examples:
nb_year(1500, 5, 100, 5000) -> 15
nb_year(1500000, 2.5, 10000, 2000000) -> 10
Note: Don't forget to convert the percent parameter as a percentage in the body of your function: if the parameter percent is 2 you have to convert it to 0.02.
```



- 내풀이

```
function nbYear(p0, percent, aug, p) {
    let pct = percent / 100;
    for(let i = 0; ; i++){
      if(p0 < p){
        p0 = p0 + p0*pct + aug;
    } else {
        return i;
    }
  }  
}
```



- 다른사람풀이

```
function nbYear(p0, percent, aug, p) {
  for(var y = 0; p0 < p; y++) p0 = p0 * (1 + percent / 100) + aug;
  return y;
}
```

와우.다시 정리해보자.

```
function nbYear(p0, percent, aug, p) {
	for(var i = 0; p0 < p; i++){
		p0 = p0 * (1 + percent / 100) + aug;
	}
	return i;
}
```

for문의 조건으로 p0 < p라는건 그동안 생각못했었다.

와우와우와우!

이런걸 써먹어볼 기회가 그동안 5번은 넘게 있었을거야.

꼭써먹어보자.

```
function nbYear(p0, percent, aug, p) {
  return p0 >= p ? 0 : nbYear((p0 + p0 * percent/100 + aug), percent, aug, p) + 1;
}
```

와......

p0이 p보다 크거나 같다면, 0을 리턴.

그렇지않다면 nbYear((p0 + p0 * percent/100 +aug), percent, aug, p)  + 1을 리턴..



대단하다........