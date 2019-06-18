<template>
	<view>
		<phone-directory :phones="phones" @paramClick="paramClick"></phone-directory>
	</view>
</template>

<script>
	import phoneDirectory from '@/components/phone-directory/phone-directory.vue'
	export default {
		name:"phones",
		components:{
			phoneDirectory
		},
		data() {
			return {
				//示例数据
				phones:{
					
				}
			}
		},
		mounted(){
			uni.request({
				url:this.url+'baseUser/applist',
				data:{},
				header:{
					'custom-header':'hello'
				},
				success:(res)=>{
					this.phones = res.data;
				}
			})
		},
		methods : {
			paramClick (e) {
				console.log(e)
			}
		}
	}
</script>

<style>

</style>
