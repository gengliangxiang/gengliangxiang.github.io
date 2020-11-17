# vuex 基本使用

## 1. 引入

```
yarn add vuex
```

## 2. 创建 store

- 创建一个 `store` 文件夹
- 创建一个 `user.js`,内容如下

```
export default {
	namespaced: true,
	state: {
		userName: localStorage.userName || '',
		token: localStorage.token || '',
		userId: localStorage.userId || '',
		publicKey: '',
	},
	mutations: {
		updatePublicKey(state, publicKey) {
			state.publicKey = publicKey;
		},
	},
	getters: {
		getPublicKey(state) {
			return state.publicKey;
		},
	},
	actions: {
		updatePublicKey({ commit }, publicKey) {
			commit('updatePublicKey', publicKey);
		},
	},
};

```

- `store` 文件夹内创建 `index.js`内容如下

```
import Vue from 'vue';
import Vuex from 'vuex';
import userStore from '@/store/user';

Vue.use(Vuex);

export default new Vuex.Store({
	modules: {userStore},
});

```

## 3. main.js 中引入 store

```
import Vue from 'vue';
import App from './App.vue';
import router from './router';
import store from '@/store';

Vue.config.productionTip = false;

new Vue({
	router,
	store,
	render: (h) => h(App),
}).$mount('#app');

```

## 4. 在 vue 文件中使用 store

```
this.$store.state.userStore.token
```
