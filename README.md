# 토이프로젝트 투두리스트


![11](https://user-images.githubusercontent.com/127499117/236602730-4e93dd68-97fb-4f09-a666-8180f1153a5a.gif)


> ﻿투두 리스트 만들기 전초전인 두 번째 토이 프로젝트 '정말 심플한 투두 리스트'를 만들어보았다. 이전 작업물인 쇼핑리스트와 비교해보면, 입력하고 삭제하는 기능은 모두 동일하지만 로컬스토리지를 이용하여 새로고침하거나 브라우저를 껐다 켜도 리스트가 저장될 수 있게 만들었고, 삭제할때도 로컬스토리지에 저장된 값을 변경해 주어야여해서 사용자가 등록한 값마다 임의의 id 값을 부여하여, 어떤것을 삭제하는지 구별 될 수 있게 하였다.

<br/>
<br/>

## 새로 배운 것들

 <br/>

```js
 //삭제
 const onDeleteList = (e) => {
  const target = e.target;
  if (e.target.className !== 'todo_remove_button') return;
  const targetList = target.closest('li');
  targetList.remove();
  //클릭된 li의 id 값과, 로컬리스트의 아이디가 같은거 제외 리턴
  //저장된 리스트에 다시 할당해줌
  savedList = savedList.filter((list) => {
    return list.id !== parseInt(targetList.dataset.id);
  });
  //다시할당해준 값으로 로컬스토리지 업데이트해줌
  saveList();
};

});


```

## 1.filter()

- filter메서드는 자신을 호출한 배열의 모둔 요소를 순회하면서 인수로 전달 받은 콜백 함수의 반환값이 "true"인 요소로만 구성된 새로운 배열을 반환한다. 이때 원본 배열은 변경되지 않는다. 
- 배열 메서드 중 정말 많이 쓰이는 map, forEach와 리턴값을 비교해보자면, forEach는 언제나 undefined를 반환하고, map메서드는 콜백 함수의 반환 값들로 구성된 새로운 배열을 반환하지만(이때 새로운 배열과 기존배열의 길이는 같다) , filter메서드는 콜백 함수의 반환값이 true인 요소만 추출한 새로운 배열을 반환한다. (filter 메서드가 생성하여 반환한 새로운 배열의 길이는 filter메서드를 호출한 배열의 길이보다 같거나 작다.)

<br/>

```js

 //삭제
 //리스트 저장
const saveList = () => {
  localStorage.setItem(TO_DO_KEY, JSON.stringify(savedList));
};

//새로고침시 저장된 리스트 유지
if (getSavedList) {
  const parsedTodos = JSON.parse(getSavedList);
  //새로고침하면 빈 배열이 아닌 로컬스토리지에 저장되어있는 값으로 할당
  savedList = parsedTodos;
  parsedTodos.forEach((list) => {
    createListDOM(list);
  });
}

```

## 2. JSON.stringify

- JSON.stringify 메서드는 객체를 JSON 포맷의 문자열로 변환한다. 클라이언트가 서버로 객체를 전송하려면 객체를 문자열화해야 하는데 이를 직렬화(serializing)이라 한다.
- 배열 메서드 중 정말 많이 쓰이는 map, forEach와 리턴값을 비교해보자면, forEach는 언제나 undefined를 반환하고, map메서드는 콜백 함수의 반환 값들로 구성된 새로운 배열을 반환하지만(이때 새로운 배열과 기존배열의 길이는 같다) , filter메서드는 콜백 함수의 반환값이 true인 요소만 추출한 새로운 배열을 반환한다. (filter 메서드가 생성하여 반환한 새로운 배열의 길이는 filter메서드를 호출한 배열의 길이보다 같거나 작다.)
- 로컬스토리지에 값을 저장할때는 예를들어 1,2,3 이렇게 단순히 "문자"로만 저장되기때문에, SON.stringify를 통해 ["1","2","3"] 배열의 형태로 변환해주었다.

<br/>

## 3. JSON.stringify

- JSON.parse메서드는 JSON 포맷의 문자열을 객체로 변환한다. 서버로부터 클라이언트에게 전송된 JSON 데이터는 "문자열"이다. 이 문자열을 객체로서 사용하려면 JSON 포맷의 문자열을 객체화 해야하는데 이를 역직렬화(deserializig)라고 한다.
- JSON.stringify로 배열처럼 보이게는 만들었지만, 로컬스토리지에 있는 값을 다시 자바스크립트에서 사용할 수 있는 값으로 변경해주기위해 JSON.parse 메서드를 이용해 배열로 만들어주었다. 

<br/>

## 4. JSON 표기 방식

- JSON은 자바스크립트의 객체 리터럴과 유사하게 키와 값으로 구성된 순수한 텍스트다. JSON의 키는 반드시 큰따옴표(작은따옴표 사용불가)로 묶어야한다. 값은 객체 리터럴과 같은 표기법을 그대로 사용할 수 있다. 

<br/>



