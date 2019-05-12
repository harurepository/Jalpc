---
title: "Unity Monobehaviour Lifecycle"
date: 2019-05-12 20:49:00 +0900
categori: Unity
---
유니티에 있어 가장 기본이 되고 중요한 Monobehaviour의 Lifecycle 유니티로 작업한다면 잊지 말아야 할 중요한 요소

![](http://project.toki-labs.com:83/wp-content/uploads/2018/11/Unity_Lifecycle.jpg)

여기에서 중요한 점은 FixedUpdate와 Update, LateUpdate는 그림상으로는 위에서 아래로 순차적으로 진행되는것 같지만, 실상은 FixedUpdate는 물리체킹에 사용된 고정프램임에 따라 실행되고, Update, LateUpdate는 일반적인프래임마다 호출되도록 되어 있기에 순차적으로 호출되지는 않는다. 따라서 별도의 Framerate로 돌고 있으므로 순차적으로 호출되기보단 각각의 상황에 따라 호출되게 되어있다.

Time.deltatime이 호출될경우 FixedUpdate에서는 고정프래임율이, Update, LateUpdate에서는 실제 시간을 나타나게 해준다.

OnApplicationPause는 보통 홈버튼을 누르거나 화면전환이 일어날때 발생되는 이벤트이다.
