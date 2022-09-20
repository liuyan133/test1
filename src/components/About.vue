<template>https://github.com/liuyan133/test1/blob/main/src/components/About.vue
	<div>
		<h2>中国时间2.0</h2>
		<button @click="Time">北京时间:<label>{{time}}</label></button>
	</div>
</template>

<script>
	import axios from 'axios'
	export default {
		// eslint-disable-next-line vue/multi-word-component-names
		name:'About',
		data() {
		
			return {
				keyWord:'',
				time:this.time
			}
		},
		methods: {
			Time(){
				//请求前更新List的数据
				
				axios.get(`https://api.tianapi.com/worldtime/index?key=ed9f3dfa32e378106876b410f5a45227&city=%E5%8C%97%E4%BA%AC`).then(
					response => {
						console.log('请求成功了',response.data)
						this.time = response.data.newslist[0].strtime
						//请求成功后更新List的数据
						// this.$bus.$emit('updateListData',{isLoading:false,errMsg:'',users:response.data.items})
					},
					error => {
						//请求后更新List的数据
						this.$bus.$emit('updateListData',{isLoading:false,errMsg:error.message,users:[]})
					}
				)
			}
		},
	}
</script>
