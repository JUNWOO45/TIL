# **Array.prototype.includes** vs **Array.prototype.indexOf**



## Usual

---

### indexOf

```javascript
const arr = [1, 2, 3, 4, 5];

if(arr.indexOf(4) > -1) {
  console.log('in the array!');
}
```



###includes

```javascript
const arr = [1, 2, 3, 4, 5];

if(arr.includes(4)) {
  console.log('in the array!');
}
```



## NaN

---

### indexOf

```javascript
const arr = [NaN];
console.log(arr.indexOf(NaN));	//-1
```



###includes

```javascript
const arr = [NaN];
console.log(arr.includes(NaN));	//true
```



## undefined

---

### indexOf

```javascript
const arr = [ , , , ];
console.log(arr.indexOf(undefined));	//-1
```



### includes

```javascript
const arr = [ , , ,];
console.log(arr.includes(undefined));	//true
```



