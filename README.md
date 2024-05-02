# HW#1
## chap.1
### 예제1-1(변수 선언)
```
var a;
```
변경 가능한 데이터가 담길 수 있는 공간인 변수를 선언.
### 예제1-2(변수 선언과 할당)
```
var a;
a='abc';

var a='abc';
```
변수를 선언하고 변수에 데이터를 할당하든, 변수를 선언함과 동시에 데이터를 할당하든 자바스크립트 엔진은 같은 동작을 수행함.
### 예제1-3(불변성)
```
var a= 'abc';
a=a+'def';

var b=5;
var c=5;
b=7;
```
변수에 어떠한 값을 할당했다가 그 값을 바꾸게 된다면 기존의 있는 값을 없애거나 대체하는 것이 아닌 기존의 값은 그대로 두고 새로운 값을
만들어서 그 값을 변수에 저장함. 기존에 있던 값은 가비지 컬렉팅을 하지 않는 한 영원히 변하지 않음.
### 예제1-4(참조형 데이터의 할당)
```
var obj1={
    a:1,
    b:'bbb'
};
```
참조형 데이터는 기본형 데이터와 다르게 '객체의 변수(프로퍼티) 영역'이 별도로 존재함. 데이터 영역에 저장된 값은 모두 불변값임.
### 예제1-5(참조형 데이터의 프로퍼티 재할당)
```
var obj1={
    a:1,
    b:'bbb'
};
obj1.a=2;
```
참조형 데이터의 프로퍼티를 재할당 하게 되면 변수가 바라보고 있는 주소는 변하지 않음. 기존의 객채 내부의 값만 바뀌게 됨.
### 예제1-6(중첩된 참조형 데이터(객체)의 프로퍼티 할당)
```
var obj={
    x:3,
    arr:[3,4,5]
};
```
참조형 데이터 안에 데이터 그룹을 넣게 되면 중첩이 되어 객체의 값이 저장되어야 하는 곳에 중첩된 데이터의 주소를 넣게 됨.
### 예제1-7(변수 복사)
```
var a = 10;
var b = a;

var obj1 = { c: 10, d: 'ddd'};
var obj2 = obj1;
```
변수를 복사하면 새로운 공간에 데이터를 저장하는 것이 아닌 데이터가 저장되어있는 주소를 붙여넣게 됨.
### 예제1-8(변수 복사 이후 값 변경 결과 비교
```
var a=10;
var b=a;
var obj1={c:10,d:'ddd'};
var obj2=obj1;

b=15;
obj2.c=20;
```
변수 복사 이후에 값을 변경하게 되면 기본형 데이터의 경우 데이터의 주소값이 변경되지만 참조형 데이터의 경우 데이터의 주소값은 변하지 
않음.
### 예제1-9(변수 복사 이후 값 변경 결과 비교(2)-객체 자체를 변경했을 때)
```
var a=10;
var b=a;
var obj1={c:10,d:'ddd'};
var obj2=obj1;

b=15;
obj={c:20,d:'ddd'};
```
변수 복사를 하고 이후 값 변경을 할 때 참조형 데이터의 경우 새로운 객체를 할당하게 되면 객체에 대한 변경임에도 값이 바뀌게 됨.
### 예제1-10(객체의 가변성에 따른 문제점)
```
var user={
    name: 'yeseong',
    gender: 'male'
};
var changeName = function(user,newName){
    var newUser=user;
    newUser.name=newName;
    return newUser;
};

var user2=changeName(user,'Shin');

if(user!==user2){
    console.log('유저 정보가 변경되었습니다!');
}
console.log(user.name, user2.name);
console.log(user===user2);
```
위의 예시로는 정보가 바뀐 시점에서 알림을 보내거나, 바뀌기 전의 정보와 바뀐 후의 정보의 차이를 가시적으로 보여주는 기능을 구현하기엔 어려움.
### 예제1-11(객체의 가변성에 따른 문제점의 해결 방법)
```
var user ={
    name: 'yeseong',
    gender:'male'
};

var changeName=function(user,newName){
    return{
        name:newName,
        gender:user.gender
    };
};

var user2=changeName(user,'Shin');

if(user!==user2){
    console.log('유저 정보가 변경되었습니다.');
}
```
예제1-10과 다르게 changeName함수에서 새로운 객체를 반환하도록 수정함. 이제 안전하게 변경 전고 후를 비교할 수 있음. 그러나 변경해야 할 정보가 많을수록 입력하는 수고가 늘어나게 됨.
### 예제1-12(기존 정보를 복사해서 새로운 객체를 반환하는 함수(얕은 복사))
```
var copyObject=function(target){
    var result={};
    for(var prop in target){
        result[prop]=target[prop];
    }
    return result;
};
```
copyObject라는 함수는 for in 문법을 이용해 result객체에 target객체의 프로퍼티들을 복사하는 함수임.
### 예제1-13(copyObject를 이용한 객체 복사)
```
var copyObject=function(target){
    var result={};
    for(var prop in target){
        result[prop]=target[prop];
    }
    return result;
};
var user={
    name:'Yeseong',
    gender:'male'
};

var user2=copyObject(user);
user2.name='Shin';

if(user!==user2){
    console.log('유저 정보가 변경되었습니다!');
}
console.log(user.name,user2.name);
console.log(user===user2);
```
copyObject 함수를 통해 객체를 복사하고 내용을 수정함. 얕은 복사만을 수행한다는 점이 아쉬움.
### 예제1-14(중첩된 객체에 대한 얕은 복사)
```
var copyObject=function(target){
    var result={};
    for(var prop in target){
        result[prop]=target[prop];
    }
    return result;
};

var user={
    name:'Yeseong',
    urls:{
        portfolio:'http://github.com/abc',
        blog:'http://blog.com',
        facebook:'http://facebook.com/abc'
    }
};
var user2=copyObject(user);

user2.name='Shin';
console.log(user.name===user2.name);

user.urls.portfolio='http://portfolio.com';
console.log(user.urls.portfolio===user2.urls.portfolio);

user2.urls.blog='';
console.log(user.urls.blog===user2.urls.blog);
```
위의 코드에선 user 객체에 직접 속한 프로퍼티에 대해서는 복사해서 완전히 새로운 데이터가 만들어진 반면, 한 단계 더 들어간 urls의 내부 프로퍼티들은 기존 데이터를 그대로 참조함.
### 예제1-15(중첩된 객체에 대한 깊은 복사)
```
var copyObject=function(target){
    var result={};
    for(var prop in target){
        result[prop]=target[prop];
    }
    return result;
};

var user={
    name:'Yeseong',
    urls:{
        portfolio:'http://github.com/abc',
        blog:'http://blog.com',
        facebook:'http://facebook.com/abc'
    }
};

var user2=copyObject(user);
user2.urls=copyObject(user.urls);

user.urls.portfolio='http://portfolio.com';
console.log(user.urls.portfolio===user2.urls.portfolio);

user2.urls.blog='';
console.log(user.urls.blog===user2.urls.blog);
```
어떠한 객체를 복사할 때 객체 내부의 모든 값을 복사해서 완전히 새로운 데이터를 만들고자 할 때, 객체의 프로퍼티 중에서 그 값이 기본형 데이터일 경우에는 그대로 복사하면 되지만 참조형 데이터는
다시 그 내부의 프로퍼티들을 복사해야 함.
### 예제1-16(객체의 깊은 복사를 수행하는 범용 함수)
```
var copyObjectDeep=function(target){
    var result={};
    if(typeof target==='object'&&target!==null){
        for(var prop in target){
            result[prop]=copyObjectDeep(target[prop]);
        }
    } else{
        result=target;
    }
    return result;
};
```
위의 코드에서는 객체를 복사한 다음에는 원본과 사본이 서로 완전히 다른 객체를 참조하게 되어 어느 쪽의 프로퍼티를 변경하더라도 다른 쪽에 영향을
주지 않음.
### 예제1-17(깊은 복사 결과 확인)
```
var copyObjectDeep = function(target) {
    var result = {};
    if (typeof target === 'object' && target !== null) {
      for (var prop in target) {
        result[prop] = copyObjectDeep(target[prop]);
      }
    } else {
      result = target;
    }
    return result;
  };
  
  var obj = {
    a: 1,
    b: {
      c: null,
      d: [1, 2]
    }
  };
  var obj2 = copyObjectDeep(obj);
  
  obj2.a = 3;
  obj2.b.c = 4;
  obj.b.d[1] = 3;
  
  console.log(JSON.stringify(obj));
  console.log(JSON.stringify(obj2));
```
깊은 복사의 결과를 확인함.
### 예제1-18(JSON을 활용한 간단한 깊은 복사)
```
var copyObjectViaJSON=function(target){
    return JSON.parse(JSON.stringify(target));
};
var obj={
    a:1,
    b:{
        c:null,
        d:[1,2],
        func:function(){console.log(3);}
    },
    func2:function(){console.log(4);}
};
var obj2=copyObjectViaJSON(obj);

obj2.a=3;
obj2.b.c=4;
obj.b.d[1]=3;

console.log(JSON.stringify(obj));
console.log(JSON.stringify(obj2));
```
객체를 JSON문법으로 표현된 문자열로 전환 했다가 다시 JSON객체로 바꾸는 방법. 순수한 정보만 다룰 때 활용하기 좋음.
### 예제1-19(자동으로 undefined를 부여하는 경우)
```
var a;
console.log(a);

var obj={a:1};
console.log(obj.a);
console.log(obj.b);
console.log(b);

var func=function(){};
var c=func();
console.log(c);
```
자바스크립트 엔진이 자동으로 undefined를 부여하는 경우.
### 예제1-20(undefined와 배열)
```
var arr1=[];
arr1.length=3;
console.log(arr1);

var arr2=new Array(3);
console.log(arr2);

var arr3=[undefined,undefined,undefined];
console.log(arr3);
```
'비어있는 요소'와 'undefined를 할당한 요소'는 출력 결과가 다름. '비어있는 요소'는 순회와 관련된 많은 배열 메서드들의 순회 대상에서 제외됨.
### 예제1-21(빈 요소와 배열의 순회)
```
var arr1=[undefined,1];
var arr2=[];
arr2[1]=1;

arr1.forEach(function (v, i) {console.log(v,i);});
arr2.forEach(function(v,i){console.log(v,i);});

arr1.map(function(v,i){return v+i;});
arr2.map(function(v,i){return v+i;});

arr1.filter(function(v){return !v;});
arr2.filter(function(v){return !v;});

arr1.reduce(function(p,c,i){return p+c+i;},'');
arr2.reduce(function(p,c,i){return p+c+i;},'');
```
arr1에 대해서는 배열의 모든 요소를 순회해서 결과를 출력. arr2는 각 메서드들이 비어있는 요소에 대해서는 어떠한 처리도 하지 않고 건너뜀.
### 예제1-22(undefined와 null의 비교)
```
var n=null;
console.log(typeof n);

console.log(n==undefined);

console.log(n==null);

console.log(n===undefined);
console.log(n===null);
```
어떤 변수가 실제로 null인지 아니면 undefined인지는 동등 연사자로 비교해서는 알 수 없음.
## chap.2
### 예제2-1(실행 컨텍스트와 콜 스택)
```
var a=1;
function outer(){
    function inner(){
        console.log(a);
        var a=3;
    }
    inner();
    console.log(a);
}
outer();
console.log(a);
```
자동으로 생성되는 전역공간과 악마로 취급받는 eval을 제외하면 우리가 흔히 실행 컨텍스트를 구성하는 방법은 함수를 실행하는 것뿐임.
### 예제2-2(매개변수와 변수에 대한 호이스팅(1)-원본코드)
```
function a(x){
    console.log(x);
    var x;
    console.log(x);
    var x=2;
    console.log(x);
}
a(1);
```
인자들과 함께 함수들을 호출한 경우의 동작을 살펴보면, arguments에 전달 된 인자를 담는 것을 제외하면 코드 내부에서 변수를 선언한 것과 다른 점이 없음.
### 예제2-3(매개변수와 변수에 대한 호이스팅(2)-매개변수를 변수 선언/할당과 같다고 간주해서 변환한 상태)
```
function a(x){
    var x=1;
    console.log(x);
    var x;
    console.log(x);
    var x=2;
    console.log(x);
}
a();
```
인자를 함수 내부의 다른 코드보다 먼저 선언 및 할당이 이뤄진 것으로 간주 할 수 있음.
### 예제2-4(매개변수와 변수에 대한 호이스팅(3)-호이스팅을 마친 상태)
```
function a(){
    var x;
    var x;
    var x;

    x=1;
    console.log(x);
    console.log(x);
    x=2;
    console.log(x);
}
a(1);
```
enviromentRecord는 현재 실행될 컨텍스트의 대상 코드 내에 어떤 식별자들이 있는지에만 관심이 있고, 각 식별자에 어떤 값이 할당될 것인지는 관심이 없음. 변수를 호이스팅할 때 변수명만
끌어올리고 할당 과정은 원래 자리에 그대로 남겨둠.
### 예제2-5(함수 선언의 호이스팅(1)-원본 코드)
```
function a(){
    console.log(b);
    var b='bbb';
    console.log(b);
    function b(){}
    console.log(b);
}
a();
```
변수는 선언부와 할당부를 나누어 선언부만 끌어올리는 반면 함수 선언은 함수 전체를 끌어올림.
### 예제2-6(함수 선언의 호이스팅(2)-호이스팅을 마친 상태)
```
function a(){
    var b;
    function b() {}

    console.log(b);
    b='bbb';
    console.log(b);
    console.log(b);
}
a();
```
예제2-5의 코드에서 수집대상1과 2를 순서대로 끌어올리고 나면 위의 코드와 같은 형태로 변환됨.
### 예제2-7(함수 선언의 호이스팅(3)-함수 선언문을 함수 표현식으로 바꾼 코드)
```
function a(){
    var b;
    var b=function b(){ }

    console.log(b);
    b='bbb';
    console.log(b);
    console.log(b);
}
a();
```
호이스팅을 고려하지 않은 상태에서 예상하기로는 (1)에러,(2)'bbb',(3)b함수 가 나올것으로 예상했지만 실제로는 (1)b함수,(2)'bbb',(3)'bbb' 라는 결과를 확인 할 수 있음.
### 예제2-8(함수를 정의하는 세 가지 방식)
```
function a() {/*...*/}
a();

var b= function () {/*...*/}
b();

var c= function d () {/*...*/}
c();
d();
```
함수 선언문, (익명)함수 표현식, 기명 함수 표현식처럼 세가지 방식으로 함수를 정의할 수 있음.
### 예제2-9(함수 선언문과 함수 표현식(1)-원본 코드)
```
console.log(sum(1,2));
console.log(multiply(3,4));

function sum(a,b){
    return a+b;
}

var multiply=function(a,b){
    return a * b;
}
```
실행 컨텍스트의 lexicalEnviroment는 두 가지 정보를 수집하는데, 그중에 enviromentRecord의 정보 수집 과정에서 발생하는 호이스팅을 살펴보는 중.
### 예제2-10(함수 선언문과 함수 표현식(2)-호이스팅을 마친 상태)
```
var sum=function sum(a,b){
    return a+b;
};
var multiply;
console.log(sum(1,2));
console.log(multiply(3,4));

multiply=function(a,b){
    return a*b;
};
```
함수 선언문은 전체를 호이스팅한 반면 함수 표현식은 변수 선언부만 호이스팅함. 함수도 하나의 값으로 취급할 수 있음.
### 예제2-11(함수 선언문의 위험성)
```
console.log(sum(3,4));

function sum (x,y){
    return x+y;
}

var a = sum(1,2);

function sum (x,y){
    return x+'+'+y+'='+(x+y);
}

var c=sum(1,2);
console.log(c);
```
전역 컨텍스트가 활성화될 때 전역공간에 선언된 함수들이 모두 가장 위로 끌어올려짐. 동일한 변수명에 서로 다른 값을 할당할 경우 나중에 할당한 값이
먼저 할당한 값을 덮어씌움. 따라서 실제 호출되는 함수는 마지막에 선언된 함수 뿐임.
### 예제2-12(상대적으로 함수 표현식이 안전하다.)
```
console.log(sum(3,4));

var sum = function(x,y){
    return x+y;
};

var a=sum(1,2);

var sum= function(x,y){
    return x+'+'+y+'='+(x+y);
};

var c=sum(1,2);
console.log(c);
```
전역공간에 동명의 함수가 여럿 존재하는 상황이라 하더라도 모든 함수가 함수 표현식으로 정의돼 있었다면 문제가 생기지 않음.
### 예제2-13(스코프 체인)
```
var a=1;
var outer=function(){
    var inner=function(){
        console.log(a);
        var a=3;
    };
    inner();
    console.log(a);
};
outer();
console.log(a);
```
여러 스코프에서 동일한 식별자를 선언한 경우에는 무조건 스코프 체인 상에서 가장 먼저 발견된 식별자에만 접근 가능함.
### 예제2-14(스코프 체인 확인(1)-크롬전용)
```
var a=1;
var outer=function(){
    var b=2;
    var inner=function(){
        console.dir(inner);
    };
    inner();
};
outer();
```
### 예제2-15(스코프 체인 확인(2)-크롬전용)
```
var a=1;
var outer=function(){
    var b=2;
    var inner=function(){
        console.log(b);
        console.dir(inner);
    };
    inner();
};
outer();
```
### 예제2-16(스코프 체인 확인(3)-크롬전용)
```
var a=1;
var outer=function(){
    var b=2;
    var inner=function(){
        console.log(b);
        debugger;
    };
    inner();
};
outer();
```
## chap.3
### 예제3-1(전역 공간에서의 this(브라우저 환경))
```
console.log(this);
console.log(window);
console.log(this===window);
```
전역 공간에서 this는 전역 객체를 가리킴. 브라우저 환경에서 전역객체는 window임.
### 예제3-2(전역 공간에서의 this(Node.js환경)
```
console.log(this);
console.log(global);
console.log(this === global);
```
Node.js환경에서 전역객체는 global임.
### 예제3-3(전역변수와 전역객체(1))
```
var a=1;
console.log(a);
console.log(window.a);
console.log(this.a);
```
사용자가 var연산자를 이용해 변수를 선언하더라도 실제 자바스크립트 엔진은 어떤 특정 객체의 프로퍼티로 인식하는 것입니다. 특정 객체란 바로 실행 컨텍스트의 LexicalEnviroment(이하 L.E)임. 실행 컨텍스트는
변수를 수집해서 L.E의 프로퍼티로 저장함. 이후 어떤 변수를 호출하면 L.E를 조회해서 일치하는 프로퍼티가 있을 경우 그 값을 반환함. 전역 컨텍스트의 경우 L.E는 전역객체를 그대로 참조함.
### 예제3-4(전역변수와 전역객체(2))
```
var a=1;
window.b=2;
console.log(a, window.a, this.a);
console.log(b, window.b, this.b);

window.a=3;
b=4;
console.log(a,window.a,this.a);
console.log(b,window.b,this.b);
```
대부분의 경우에 전역 공간에서는 var로 변수를 선언하는 대신 window의 프로퍼티에 직접 할당하더라도 결과적으로 var로 선언한 것과 똑같이 동작함.
### 예제3-5(전역변수와 전역객체(3))
```
var a=1;
delete window.a;
console.log(a,window.a,this.a);

var b=2;
delete b;
console.log(b,window.b,this.b);

window.c=3;
delete window.c;
console.log(c, window.c, this.c);

window.d=4;
delete d;
console.log(d,window.d,this.d);
```
처음부터 전역객체의 프로퍼티로 할당한 경우에는 삭제가 되는 반면 전역변수로 선언한 경우에는 삭제가 되지 않음.
전역변수를 선언하면 자바스크립트 엔진이 이를 자동으로 전역객체의 프로퍼티로 할당하면서 추가적으로 해당 프로퍼티의 configurable속성(변경 및 삭제 가능성)을 false로 정의함.
### 예제3-6(함수로서 호출, 메서드로서 호출)
```
var func=func=function(x){
    console.log(this,x);
};

func(1);

var obj={
    method:func
};
obj.method(2);
```
앞에 점이 없으면 함수로서 호출한 것이고, 앞에 점이 있으면 메서드로서 호출한 것임.
### 예제3-7(메서드로서 호출-점 표기법, 대괄호 표기법)
```
var obj={
    method:function(x){console.log(this,x);}
};
obj.method(1);
obj['method'](2);
```
어떤 함수를 호출할 때 그 함수 이름앞에 객체가 명시돼 있는 경우에는 메서드로 호출한 것이고, 그렇지 않은 경우에는 함수로 호출한 것임.
### 예제3-8(메서드 내부에서의 this)
```
var obj={
    methodA:function(){console.log(this);},
    inner:{
        methodB:function(){console.log(this);}
    }
};
obj.methodA();
obj['methodA']();

obj.inner.methodB();
obj.inner['methodB']();
obj['inner'].methodB();
obj['inner']['methodB']();
```
어떤 함수를 메서드로서 호출하는 경우 호출 주체는 바로 함수명 앞의 객체임. 점 표기법의 경우 마지막 점 앞에 명시된 객체가 곧 this가 되는 것임.
### 예제3-9(내부함수에서의 this)
```
var obj1={
    outer: function(){
        console.log(this);
        var innerFunc=function(){
            console.log(this);
        }
        innerFunc();

        var obj2={
            innerMethod: innerFunc
        };
        obj2.innerMethod();
    }
};
obj1.outer();
```
this 바인딩에 관해서는 함수를 실행하는 당시의 주변환경은 중요하지 않고, 오직 해당 함수를 호출하는 구문앞에 점 또는 대괄호 표기가 있는지 없는지가 관건임.
### 예제3-10(내부함수에서의 this를 우회하는 방법)
```
var obj={
    outer:function(){
        console.log(this);
        var innerFunc1=function(){
            console.log(this);
        };
        innerFunc1();

        var self=this;
        var innerFunc2=function(){
            console.log(self);
        };
        innerFunc2();
    }
};
obj.outer();
```
ES5까지는 자체적으로 내부함수에 this를 상속할 방법이 없지만 변수를 활용하여 우회를 할 수가 있음.
### 예제3-11(this를 바인딩 하지 않는 함수(화살표 함수))
```
var obj={
    outer:function(){
        console.log(this);
        var innerFunc=() =>{
            console.log(this);
        };
        innerFunc();
    }
};
obj.outer();
```
ES6에서는 함수 내부에서 this가 전역객체를 바라보는 문제를 보완하고자, this를 바인딩 하지 않는 화살표 함수를 새로 도입함.
화살표 함수는 실행 컨텍스트를 생서할 때 this바인딩 과정 자체가 빠지게 되어, 상위 스코프의 this를 그대로 활용할 수 있음.
### 예제3-12(콜백 함수 내부에서의 this)
```
setTimeout(function(){console.log(this);},300);

[1,2,3,4,5].forEach(function(x){
    console.log(this,x);
});

document.body.innerHTML +='<button id="a"클릭</button>';
document.body.querySelector('#a')
    .addEventListener('click',function(e){
        console.log(this,e);
    });
```
콜백 함수의 제어권을 가지는 함수가 콜백 함수에서의 this를 무엇으로 할지 결정하며, 특별히 정의하지 않은 경우에는 기본적으로 함수와 마찬가지로 전역객체를 바라봄.
### 예제3-13(생성자 함수)
```
var Cat=function(name,age){
    this.bark='야옹';
    this.name=name;
    this.age=age;
};
var choco = new Cat('초코',7);
var nabi = new Cat('나비',5);
console.log(choco,nabi);
```
생성자 함수를 호출하면 우선 생성자의 prototype 프로퍼티를 참조하는 __proto__라는 프로퍼티가 있는 객체를 만들고,
미리 준비된 공통 속성 및 개성을 해당 객체에 부여함.
### 예제3-14(call 메서드(1))
```
var func=function(a,b,c){
    console.log(this,a,b,c);
};

func(1,2,3);
func.call({x:1},4,5,6);
```
함수를 그냥 실행하면 this는 전역객체를 참조하지만 call 메서드를 이용하면 임의의 객체를 this로 지정할 수 있음.
### 예제3-15(call 메서드(2))
```
var obj={
    a:1,
    method:function(x,y){
        console.log(this.a,x,y);
    }
};

obj.method(2,3);
obj.method.call({a:4},5,6);
```
객체의 메서드를 그냥 호출하면 this는 객체를 참조하지만 call 메서드를 이용하면 임의의 객체를 this로 지정할 수 있음.
### 예제3-16(apply 메서드)
```
var func=function(a,b,c){
    console.log(this,a,b,c);
};
func.apply({x:1},[4,5,6]);

var obj={
    a:1,
    method:function(x,y){
        console.log(this.a,x,y);
    }
};
obj.method.apply({a:4},[5,6]);
```
call 메서드는 첫 번째 인자를 제외한 나머지 모든 인자들을 호출할 함수의 매개변수로 지정하는 반변, apply 메서드는 두 번째 인자를 배열로 받아 그 배열의 요소들을 호출할 함수의 매개변수로 지정한다는 차이가 있음.
### 예제3-17(call/apply 메서드의 활용 1-1)유사배열객체에 배열 메서드를 적용)
```
var obj={
    0:'a',
    1:'b',
    2:'c',
    length:3
};
Array.prototype.push.call(obj,'d');
console.log(obj);

var arr=Array.prototype.slice.call(obj);
console.log(arr);
```
객체에는 배열 메서드를 직접 적용할 수 없음. 그러나 키가 0 또는 양의 정수인 프로퍼티가 존재하고 length 프로퍼티의 값이 0 또는 양의 정수인 객체, 즉 배열의 구조와 유사한 객체의 경우
call 또는 apply 메서드를 이용해 배열 메서드를 차용할 수 있음.
### 예제3-18(call/apply 메서드의 활용 1-2)arguments,NodeList에 배열 메서드를 적용)
```
function a(){
    var argv=Array.prototype.slice.call(arguments);
    argv.forEach(function(arg){
        console.log(arg);
    });
}
a(1,2,3);

document.body.innerHTML='<div>a</div><div>b</div><div>c</div>';
var nodeList=document.querySelectorAll('div');
var nodeArr=Array.prototype.slice.call(nodeList);
nodeArr.forEach(function(node){
    console.log(node);
});
```
함수 내부에서 접근할 수 있는 arguments 객체도 유사배열객체이므로 배열로 전환해서 활용할 수 있음. NodeList도 마찬가지.
### 예제3-19(call/apply메서드의 활용 1-3)문자열에 배열 메서드 적용 예시)
```
var str='abc def';

Array.prototype.push.call(str,',pushed string');

Array.prototype.concat.call(str,'string');

Array.prototype.every.call(str,function(char){return char !=='';});

Array.prototype.some.call(str,function(char){return char !=='';});

var newArr=Array.prototype.map.call(str,function(char){return char+'!';});

console.log(newArr);

var newStr = Array.prototype.reduce.apply(str,[
    function(string,char,i) {return string+char+i;},
    ''
]);
console.log(newStr);
```
유사배열객체는 call/apply 메서드를 이용해 모든 배열 메서드를 적용할 수 있음. 배열처럼 인덱스와 length프로퍼티를 지니는 문자열에 대해서도 마찬가지임.
단, 문자열의 경우 length프로퍼티가 읽기 전용이기 대문에 원본 문자열에 변경을 가하는 메서드는 에러를 던지며, concat처럼 대상이 반드시 배열이어야 하는 경우 제대로 된 결과를 얻을 수 없음.
### 예제3-20(call/apply 메서드의 활용 1-4)ES6의 Array.from 메서드)
```
var obj={
    0:'a',
    1:'b',
    2:'c',
    length:3
};
var arr=Array.from(obj);
console.log(arr);
```
ES6에서는 유사배열객체 또는 순회 가능한 모든 종류의 데이터 타입을 배열로 전환하는 Array.from 메서드를 새로 도입함.
### 예제3-21(call/apply 메서드의 활용 2)생성자 내부에서 다른 생성자를 호출)
```
function Person(name,gender){
    this.name=name;
    this.gender=gender;
}

function Student(name,gender,school){
    Person.call(this,name,gender);
    this.school=school;
}
function Employee(name,gender,company){
    Person.apply(this,[name,gender]);
    this.company=company;
}

var by=new Student('보영','female','단국대');
var jn=new Employee('재난','male','구골');
```
생성자 내부에 다른 생성자와 공통된 내용이 있을 경우 call 또는 apply를 이용해 다른 생성자를 호출하면 간단하게 반복을 줄일 수 있음.
### 예제3-22(call/apply 메서드의 활용 3-1)최대/최솟값을 구하는 코드를 직접 구현)
```
var numbers=[10,20,3,16,45];
var max=min=numbers[0];
numbers.forEach(function(number){
    if(number>max){
        max=number;
    }
    if(number<min){
        min=number;
    }
});
console.log(max,min);
```
배열에서 최대/최솟값을 구해야하는 경우 apply를 사용하지 않는다면 위와 같이 코드가 불필요하게 길고 가독성도 떨어짐.
### 예제3-23(call/apply 메서드 활용 3-2)여러 인수를 받는 메서드(Math.max/Math.min)에 apply를 적용
```
var numbers=[10,20,3,16,45];
var max=Math.max.apply(null,numbers);
var min=Math.min.apply(null,numbers);
console.log(max,min);
```
Math.max/Math.min 메서드에 apply를 적용하여 간단해짐.
### 예제3-24(call/apply 메서드의 활용 3-3)ES6의 펼치기 연산자 활용)
```
const numbers=[10,20,3,16,45];
const max=Math.max(...numbers);
const min=Math.min(...numbers);
console.log(max,min);
```
ES6에서는 펼치기 연산자르 이용하여 apply를 적용한 것보다 더욱 간단하게 작성할 수 있음.
### 예제3-25(bind 메서드-this 지정과 부분 적용 함수 구현)
```
var func=function(a,b,c,d){
    console.log(this,a,b,c,d);
};
func(1,2,3,4);

var bindFunc1=func.bind({x:1});
bindFunc1(5,6,7,8);

var bindFunc2=func.bind({x:1},4,5);
bindFunc2(6,7);
bindFunc2(8,9);
```
bind 메서드는 call과 비슷하지만 즉시 호출하지는 않고 넘겨 받는 this 및 인수들을 바탕으로 새로운 함수를 반환하기만 하는 메서드임.
bind 메서드는 함수에 this를 미리 적용하는 것과 부분 적용 함수를 구현하는 것 두 가지 목적을 지님.
### 예제3-26(bind 메서드-name 프로퍼티)
```
var func=function(a,b,c,d){
    console.log(this,a,b,c,d);
};
var bindFunc=func.bind({x:1},4,5);
console.log(func.name);
console.log(bindFunc.name);
```
bind 메서드를 적용해서 새로 만든 함수는 name 프로퍼티에 동사 bind의 수동태인 'bound'가 붙음. 기존의 call 이나 apply 보다 코드를 추적하기에 더 수월함.
### 예제3-27(내부함수에 this전달-call vs. bind)
```
var obj={
    outer:function(){
        console.log(this);
        var innerFunc=function(){
            console.log(this);
        };
        innerFunc.call(this);
    }
};
obj.outer();

var obj={
    outer:function(){
        console.log(this);
        var innerFunc=function(){
            console.log(this);
        }.bind(this);
        innerFunc();
    }
};
obj.outer();
```
메서드의 내부함수에서 메서드의 this를 그대로 바라보기 위한 방법으로 변수를 활용한 우회법등이 있었음. call, apply 또는 bind 메서드를 이용하면 더 깔끔하게 처리 할 수 있음.
### 예제3-28(bind메서드-내부함수에 this전달)
```
var obj={
    logThis:function(){
        console.log(this);
    },
    logThisLater1:function(){
        setTimeout(this.logThis,500);
    },
    logThisLater2:function(){
        setTimeout(this.logThis.bind(this),1000);
    }
};
obj.logThisLater1();
obj.logThisLater2();
```
콜백 함수를 인자로 받는 함수나 메서드 중에서 기본적으로 콜백 함수 내에서의 this에 관여하느 함수 또는 메서드에 대해서도 bind 메서드를 이용하면 this값을 사용자의 입맛에 맞게 바꿀 수 있음.
### 예제3-29(화살표 함수 내부에서의 this)
```
var obj={
    outer:function(){
        console.log(this);
        var innerFunc=()=>{
            console.log(this);
        };
        innerFunc();
    }
};
obj.outer();
```
예제 3-27의 내부함수를 화살표 함수로 바꾸게 되면 별도의 변수로 this를 우회하거나 call/apply/bind를 적용할 필요가 업어 더욱 간결하고 편리함.
### 예제3-30(thisArg를 받는 경우 예시-forEach메서드)
```
var report={
    sum:0,
    count:0,
    add:function(){
        var args=Array.prototype.slice.call(arguments);
        args.forEach(function(entry){
            this.sum+=entry;
            ++this.count;
        },this);
    },
    average:function(){
        return this.sum/this.count;
    }
};
report.add(60,85,95);
console.log(report.sum,report.count,report.average());
```
콜백 함수를 인자로 받는 메서드 중 일부는 추가로 this로 지정할 객체(thisArg)를 인자로 지정할 수 있는 경우가 있음. 이러한 메서드의 thisArg 값을
지정하면 콜백 함수 내부에서 this 값을 원하는 대로 변경할 수 있음. 이런 형태는 여러 내부 요소에 대해 같은 동작을 반복 수행해야 하는 배열 메서드에 많이 포진돼 있음.
### 예제3-31(콜백 함수와 함께 thisArg를 인자로 받는 메서드)
```
Array.prototype.forEach(callback[,thisArg])
Array.prototype.map(callback[,thisArg])
Array.prototype.filter(callback[,thisArg])
Array.prototype.some(callback[,thisArg])
Array.prototype.every(callback[,thisArg])
Array.prototype.find(callback[,thisArg])
Array.prototype.findIndex(callback[,thisArg])
Array.prototype.flatMap(callback[,thisArg])
Array.prototype.from(arrayLike[,callback[,thisArg]])
Set.prototype.forEach(callback[,thisArg])
Map.prototype.forEach(callback[,thisArg])
```
