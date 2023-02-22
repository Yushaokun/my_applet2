<template>
	<view data-weui-theme="theme">
	  <button class="avatar-wrapper" open-type="chooseAvatar" bind:chooseavatar="bindchooseavatar">
	    <image class="avatar" :src="avatarUrl"></image>
	  </button> 
	  <mp-form>
	    <mp-cells>
	      <mp-cell title="昵称">
	        <input type="nickname" class="weui-input" placeholder="请输入昵称"/>
	      </mp-cell>
	    </mp-cells>
	  </mp-form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// avatarUrl: "https://mmbiz.qpic.cn/mmbiz/icTdbqWNOwNRna42FI242Lcia07jQodd2FJGIYQfG0LAJGFxM4FbnQP6yfMxBgJ0F3YRqJCJ1aPAK2dQagdusBZg/0",
				avatarUrl: "",
				theme: wx.getSystemInfoSync().theme,
			}
		},
		
		onLoad() {
			wx.onThemeChange((result) => {
				// this.setData({
				// 	theme: result.theme
				// })
				uni.setStorageSync(theme, result.theme);
			})
		},
		
		methods: {
			bindchooseavatar(e) {
				// const { avatarUrl } = e.detail 
				// this.setData({
				// 	avatarUrl,
				// })
				
				this.avatarUrl = e.detail;
				console.log("avatarUrl",e.detail.avatarUrl)
				
				// const { avatarUrl } = e.detail;
				// uni.setStorageSync('user-avatar', e.detail);
			}
		}
	}
</script>

<style>
	.avatar-wrapper {
	  padding: 0;
	  width: 56px !important;
	  border-radius: 8px;
	  margin-top: 40px;
	  margin-bottom: 40px;
	}
	
	.avatar {
	  display: block;
	  width: 56px;
	  height: 56px;
	}
	
	.container {
	  display: flex;
	}
	
	.weui-input {
		text-align: center;
	}
</style>