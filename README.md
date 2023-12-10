# Javascript

## ZeroCho 강의 참고

**고차함수**

```js
const add = (a, b) => a + b;

function calculator(func, a, b){
    return func(a, b);
}

add(3,5);
console.log(add(3, 5))   // 8
console.log(calculator(add, 3, 5))  // 8

// 함수의 호출을 리턴 값으로 대체해보기 
let onClick = () => (event) => {
    console.log('hello')
}

document.querySelector('#header').addEventListener('click', onClick())

// 리턴값으로 바꿔서 생각해보기
document.querySelector('#header').addEventListener('click', (event) => {
    console.log('hello')
});
```

* 고차함수는 함수 안에서 다른 함수를 리턴함.
* 함수와 함수 호출의 차이를 정확하게 알고 넘어가자.
* 원칙은 호출을 리턴 값으로 대체해서 생각해보기.


