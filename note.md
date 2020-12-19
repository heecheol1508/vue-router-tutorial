# Vue Router



주소에 `www.mywebsite.com/user` 라고 치면

`Vue Router`가 캐치해 자신이 가지고 있는 router 중에서 user라는 이름이 있는지 찾고, user와 매칭시켜놓은 user component들을 찾게 된다.

그리고 그 component들이 user를 통해 `Vue Router`에 전달이 되고

`Vue Router`가 조합된 component들을 화면에 뿌려줌





vue는 single page application.

즉 폴더 경로대로 파일을 찾아가면서 파일을 각각 불러오는 방식이 아니라

전체 컴포넌트를 불러오고, 주소 창에 어떤 값이 입력되면 라우터가 그 입력된 값에 맞는 컴포넌트를 유저에게 보여주는 형태.





## router/index.js 컴포넌트 입력 방법

1. 컴포넌트를 import 하고 그 컴포넌트를 불러오는 방법
   - router 파일이 로딩될 때 모든 컴포넌트를 다 불러온 상태에서 주소창에 맞는 컴포넌트만 보여주는 형태
   - 속도가 느림

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/Home.vue'
import About from '../views/About.vue'

Vue.use(VueRouter)

const routes = [
    {
        path: '/',
        name: 'Home',
        component: Home
    },
    {
        path: '/about',
        name: 'About',
        component: About
    }
]

const router = new VueRouter({
    mode: 'history',
    base: process.env.BASE_URL,
    routes
})

export default router

```



2. 함수 형태로 선언하고 연결하는 방법
   - 주소와 연결된 컴포넌트 하나만 불러와서 그것만 보여줌

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/Home.vue'

Vue.use(VueRouter)

const routes = [
    {
        path: '/',
        name: 'Home',
        component: Home
    },
    {
        path: '/about',
        name: 'About',
        // route level code-splitting
        // this generates a separate chunk (about.[hash].js) for this route
        // which is lazy-loaded when the route is visited.
        component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
    }
]

const router = new VueRouter({
    mode: 'history',
    base: process.env.BASE_URL,
    routes
})

export default router

```

```javascript
// 위와 동일

import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/Home.vue'

Vue.use(VueRouter)

const About = () => {
    return import(/* webpackChunkName: "about" */ '../views/About.vue')
}

const routes = [
    {
        path: '/',
        name: 'Home',
        component: Home
    },
    {
        path: '/about',
        name: 'About',
        component: About
    }
]

const router = new VueRouter({
    mode: 'history',
    base: process.env.BASE_URL,
    routes
})

export default router

```





라우터 연결 방법들

```vue
<template>
	<h1 @click="$router.push({ name: routeName })">클릭1</h1>
	<h1 @click="$router.push({ path: routePath })">클릭2</h1>
	<h1 @click="$router.push(routePath)">클릭3</h1>

	<router-link :to="{name: routeName}">
        <h1>클릭4</h1>
    </router-link>

	<h1 router :to="{name: routeName}" exact>클릭5</h1>	//vuetify
</template>
```





라우터를 통해 값을 전달하는 방법들 중 route의 params 객체 안에 값들을 넣어서 전달하는 방법이 있다. 이렇게 params안에 값들을 넣어서 보낼수도있지만 router.js에 속성이름을 지정해줘서 (`path: "/userId/:userId"`) 주소창을 통해 값을 전달하는 방법도 있다. 

메뉴를 눌러서 들어오는 경우라면 App.vue 등 메뉴에 파라메터 값을 넣어서 전달하는 방법이 의미가 있지만, 외부에서 들어오는 사용자의 경우 파라메터를 라우터에 전달해줄 수 있는 방법이 없어서 주소창을 통해야 한다.



