6kyu



- 문제

```
The drawing below gives an idea of how to cut a given "true" rectangle into squares ("true" rectangle meaning that the two dimensions are different).

alternative text

Can you translate this drawing into an algorithm?

You will be given two dimensions

a positive integer length (parameter named lng)
a positive integer width (parameter named wdth)
You will return an array or a string (depending on the language; Shell bash and Fortran return a string) with the size of each of the squares.

  sqInRect(5, 3) should return [3, 2, 1, 1]
  sqInRect(3, 5) should return [3, 2, 1, 1]
  or (Haskell)
  squaresInRect  5  3 `shouldBe` Just [3,2,1,1]
  squaresInRect  3  5 `shouldBe` Just [3,2,1,1]
  or (Fsharp)
  squaresInRect  5  3 should return Some [3,2,1,1]
  squaresInRect  3  5 should return Some [3,2,1,1]
  or (Swift)
  squaresInRect  5  3 should return [3,2,1,1] as optional
  squaresInRect  3  5 should return [3,2,1,1] as optional
  or (Cpp)
  sqInRect(5, 3) should return {3, 2, 1, 1}
  sqInRect(3, 5) should return {3, 2, 1, 1}
  (C)
  C returns a structure, see the "Solution" and "Examples" tabs.
  Your result and the reference test solution are compared by strings.
```



- 나의풀이

```
function sqInRect(lng, wdth){
  var arr = [lng, wdth];
  var container = [];
  if(lng === wdth){
    return null;
  } else {
    for(var i = 0; ; i++){
      if(arr[0] !== arr[1] ){
        container.push(Math.min(...arr));
        arr = [Math.max(...arr) - Math.min(...arr), Math.min(...arr)];
        console.log(container,arr);
      } else {
        container.push(Math.min(...arr));
        return container;
      }
    }
  }
}
```



- 다른사람풀이

```
function sqInRect(lng, wdth){
  let arr = []
  if(lng === wdth) return null
  while(lng > 0 && wdth > 0){
    arr.push(lng > wdth ? wdth : lng)
    lng > wdth ? lng -= wdth : wdth -= lng
  }
  return arr
}
```

의도하는건 같은데, 훨씬 깔끔하다.

정리해보면,

```
function sqInRect(lng, wdth){
	let arr = [];
	if(lng === wdth){
		return null;
	}
	while(lng > 0 && wdth > 0){
		arr.push(lng > wdth ? wdth : lng)
		lng > wdth ? lng -= wdth : wdth -= lng
	}
	return arr;
}
```

