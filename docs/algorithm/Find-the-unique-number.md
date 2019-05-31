Find the unique number

문제

~~~
There is an array with some numbers. All numbers are equal except for one. Try to find it!

findUniq([ 1, 1, 1, 2, 1, 1 ]) === 2
findUniq([ 0, 0, 0.55, 0, 0 ]) === 0.55
It’s guaranteed that array contains more than 3 numbers.

The tests contain some very huge arrays, so think about performance.

This is the first kata in series:

Find the unique number (this kata)
Find the unique string
Find The Unique
~~~



나의 풀이

~~~
function findUniq(arr) {
  // do magic
  let obj = {};
  for(let i = 0; i < arr.length; i++) {
    if(obj[arr[i]]) {
      obj[arr[i]]++;
    } else {
      obj[arr[i]] = 1;
    }
  }
  console.log(Object.values(obj));
  for(let j = 0; j < Object.values(obj).length; j++) {
    if(Object.values(obj)[j] === 1) {
      return Number(Object.keys(obj)[j]);
    }
  }
}
~~~



다른사람풀이

~~~
function findUniq(arr) {
  arr.sort((a,b)=>a-b);
  return arr[0]==arr[1]?arr.pop():arr[0]
}
~~~

