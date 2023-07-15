---
title: "변수를 기억하는 방법 : localStorage"
excerpt: "js에서 변수를 local에 저장하기 위한 방법을 정리해 보았다!"

categories:
 - Blog

 tags:
  - [javascript,local Storage,variable]

toc: false
toc_sticky: false
 
date: 2023-07-15
last_modified_at: 2023-07-15
---

# 변수를 기억하는 방법 : localStorage

**창을 새로 고침 하여도 사용자가 입력한 user의 이름을 기억하려면 어떻게 해야 할까?** Local Storage API를 이용 함으로서 가능하다!  Local Storage API에는 다양한 method가 존재하는데, 그 중에서 우리가 이용할 것은 **setItem**이다. setItem을 활용해서 Local Storage에 정보를 저장할 수 있다.

```javascript
localStorage.setItem("username", "HongGilDong");
```
이 코드를 실행하면 Local Storage 에는 새로운 항목인 username이 생긴다. key는 username, value는 HongGilDong!

 ( *Local Storage의 항목은 창에서 우클릭 후 검사 -> Application -> Local Storage 을 통해 확인 할 수 있다. )*

 ***값을 설정할 때는* *localStorage.getItem("username", “HongGilDong”);*** 

***값을 불러올 때는 localStorage.getItem("username");*** 

***값을 지울 때는 localStorage.removeItem("username");***

위의 개념을  이용하여, 사용자에게 이름을 입력 받아 Local Storage에 저장하고 가져오는 함수를 만들어 본다. 만약 Local Storage에 저장 된 이름이 있다면, 입력 받는 form 은 다시 표시하지 않게 한다.

```javascript
    const loginForm = document.querySelector("#login-form"); 
    const loginInput = document.querySelector("#login-form input"); //form에서 사용자 입력이다.
    const greeting = document.querySelector("h1"); //비어있는 h1 요소이다.(인사로 채우기 위함)

    const HIDDEN_CLASSNAME = "hidden";
    const USERNAME_KEY = "username";

    function paintGreetings(username) {
        greeting.innerText = Hello ${username};
        greeting.classList.remove(HIDDEN_CLASSNAME);
    }

    function onLoginSubmit(event){
        event.preventDefault(); //이벤트의 기본 동작을 막는다(여기선 submit시의 새로고침을 막음)
        const username = loginInput.value;
        localStorage.setItem(USERNAME_KEY, username); //로컬 저장소에 입력받은 유저 이름 저장
        loginForm.classList.add("hidden");
        paintGreetings(username);
    }

    const savedUsername = localStorage.getItem(USERNAME_KEY); //로컬 저장소에 저장된 이름을 갖고 옴

    //이름의 Local Storage 저장 여부에 따라 상태를 바꾼다!

    if(savedUsername === null){ 
        loginForm.classList.remove(HIDDEN_CLASSNAME);
        loginForm.addEventListener("submit", onLoginSubmit);
    }else{
        paintGreetings(savedUsername);
    }
```
