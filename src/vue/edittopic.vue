<template>
	<nv-header></nv-header>
	<topic-box :accesstoken="accesstoken" :topic-id="topicId"></topic-box>
</template>
<script>
	import nvHeader from '../components/header.vue';
	import topicbox from '../components/topicbox.vue';
	import store from '../vuex/store';
	import {getLoginState, getUserInfo} from '../vuex/getters';
	export default {
		data : function() {
			return {
				accesstoken : this.ache_getUserInfo.accesstoken,
				topicId : ''
			}
		},
		route : {
			data (transition) {
				if(!this.ache_userLoginState) {
					// 未登陆，跳转登陆页
					this.$route.router.go({name : 'login'});
					return;
				}
				this.topicId = transition.to.params.id;
			}
		},
		components : {
			'nv-header' : nvHeader,
			'topic-box' : topicbox
		},
		store : store,
		vuex : {
			getters : {
				ache_userLoginState : getLoginState,
				ache_getUserInfo :  getUserInfo
			}
		}
	}
</script>