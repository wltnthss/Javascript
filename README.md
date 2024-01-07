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

**this**

```js
// 1. 앞에 객체를 붙여 호출하는 경우
let obj = {
    name : 'son',
    sayName() {
        console.log(this.name)  // son
    }
};
obj.sayName();

// 2. 생성자 함수를 통해서 호출하는 경우
function Human(name){
    this.name = name;
}
let man = new Human('son')
console.log(man)    // 객체 자기 자신

// 3. bind, call, apply 를 통해 변하는 경우
// bind, call, apply
function sayName(){
    console.log(this.name)
}
sayName.bind({name : 'Son'})()
sayName.call({name : 'SOn'})
sayName.apply({name: 'SON'})

// 내부함수가 같이 있는 this
let obj2 = {
    name : 'son',
    sayName(){
        console.log(this.name); // 함수 호출할 때 obj2.sayName 이므로 this는 son
        function inner() {
            console.log(this.name)
        }
        inner();    // 어떠한 this를 바꿔주는 동작이 없으므로 window.name
    }
}
console.log(obj2.sayName())

// 화살표 함수를 통해 호출하는 경우
let obj3 = {
    name : 'son',
    sayName(){
        console.log(this.name); // son
        let inner = () => {
            console.log(this.name)  // son
        }
        inner();    // 화살표 함수이므로 부모 함수의 this를 가져옴
    }
}
console.log(obj3.sayName())
```
* this는 함수를 호출할 때 정해짐.
* this는 기본적으로 window 를 뜻하지만 바뀌는 경우가 몇 가지 있음. ( 몇 가지 경우를 외워두자.)
* 앞에 객체를 붙여 호출하는 경우(객체의 메서드를 호출하는 경우), 생성자를 new로 호출하는 경우, call, bind, apply 하는 경우, 화살표함수
* strict mode 에서는 undefined 로 나옴.
* 화살표함수는 부모함수의 this를 직접 가져옴.

```js
header.addEventListener('click', function(){
    console.log(this);  // hedaer
})
```

* 여기서의 this의 정답은 알수없다. 하지만 addEventListener은 일반적으로 공식문서를 보았을 때 this는 앞에 붙은 header 지칭해줌.

```js
let hedaer = {
    addEventListener(eventName, callback){
        callback.call(header)   // this를 header로 지정
        //callback();   // this는 window
    }
}
```

* 그냥 callback()함수를 호출했을 때 this는 window가 되므로,  call을 통해 호출하여 this를 바꿔주자.

**콜백함수**

* 매개변수로 함수 객체를 전달해서 호출 함수 내에서 
매개변수 함수를 실행하는 것 

```js
function sayHello(name, age, func){
    const words = 'Hello ' + name + ' ' + age

    func(words)
}

sayHello('Son', '29', function(w){
    console.log(w)  // Hello Son 29
})

// sayHello('Son', '29', function printing(w){
//     console.log(w)  // Hello Son 29
// })
```

* 함수 자체를 전달 함으로써 굳이 함수의 이름을 명시할 필요 없이 익명 함수의 형태로 넣어주게됨.

```js
// 화살표 함수 콜백
function arrowFunc(func){
    const name = 'Park';
    func(name)
}

arrowFunc((n) => {
    console.log("Hello " + n)   // Hello Park
})

// 화살표 함수 콜백
let numbers = [1,2,3,4,5]
let arr = []

numbers.forEach((n) => {
    arr.push(n * 2)
})

console.log(arr);   //[2,4,6,8,10]
```

* 화살표 모양 함수의 형태를 고차함수내에서 콜백 함수 형태로 사용함.

```js
// 1. 이벤트 리스너 사용
let button = document.getElementById("button"); 

// 버튼에 클릭 이벤트 리스너를 추가
button.addEventListener("click", function () { // 콜백 함수
  console.log("Button clicked!"); 
});

// 2. setTimeout 사용
setTimeout(function () {
  console.log("Time is up!"); // 콜백 함수로 콘솔에 메시지 출력
}, 3000);
```

