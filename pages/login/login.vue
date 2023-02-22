<template>
	<view class="bg">
		<image src="https://www.ncky2020.top/static/wx_index.jpg" mode="aspectFill" class="bg-img"></image>
		<image src="https://www.ncky2020.top/static/banner.jpg" mode="widthFix" class="banner" @click="navitoIndex"></image>
		
		
		<button @click="startChat" class="cu-btn bg-grey lg">开始聊天</button>
		<!-- <button class="avatar-wrapper" open-type="chooseAvatar" @chooseavatar="onChooseAvatar">
			选择头像
		</button> -->
		
		<!-- 绑定用户头像与昵称 -->
		<!-- <button @click="bind_avatar" class="cu-btn bg-grey lg">绑定头像</button> -->
		
		
		<!-- 用户登录 -->
<!-- 		<button open-type="getUserInfo" bindgetuserinfo="getUserInfo">用户登录</button> -->		
		<!-- <button open-type="getUserInfo" @getuserinfo="getUserInfo" withCredentials="true" class="cu-btn bg-grey lg">用户登录</button> -->
 
		<button @click="navitoContact" class="cu-btn bg-grey lg">反馈问题</button>
		
 
		<button @click="showQrcode" class="cu-btn bg-grey lg">联系方式</button>
		<uni-popup ref="popup" type="center">
			<view class="qr-code">
				<!-- <image src="../../static/business_card.png" mode="aspectFit"></image> -->
				<image src="https://www.ncky2020.top/static/business_card.png" mode="aspectFit"></image>
			</view>
		</uni-popup>
		
		<view class="tips">
			<p align="center">Hint：这是一个智能聊天机器人 🤖 </p>
			<p align="center">试着问他一些自然、人文、地理、计算机方面的问题</p>
		</view>
		
		<!-- 此处插入广告 -->
		<!-- <view class="advertising">
			<ad unit-id="">xxx</ad>
		</view> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				avatarUrl: '',
			}
		},
		onLoad() {
			wx.showShareMenu({
				withShareTicket: true,
				//设置下方的Menus菜单，才能够让发送给朋友与分享到朋友圈两个按钮可以点击
				menus: ["shareAppMessage", "shareTimeline"]
			});
			// 	this.userAuthorized();
		},
		methods: {
			showQrcode() {
				this.$refs.popup.open('center');
			},
			onChooseAvatar(e) {
				uni.setStorageSync('user-avatar', e.detail.avatarUrl);
				setTimeout(() => {
					uni.navigateTo({
						url: '/pages/index/index'
					})
				}, 300);
	
			},
			startChat() {
				uni.navigateTo({
					url: '/pages/index/index'
				});
			},
			navitoIndex(e) {
				uni.navigateTo({
					url: '/pages/index/index'
				});
			},
			navitoContact(e) {
				uni.navigateTo({
					url: '/pages/contact/contact'
				});
			},
			bind_avatar() {
				uni.navigateTo({
					url: '/pages/bind_avatar/bind_avatar'
				});
			},
			getUserInfo() {
				// uni.getUserProfile({
				// 	desc: '用于展示您的头像与微信昵称',
				// 	lang: 'zh_CN',
				// 	success: res => {
				// 	    console.log(res);
				// 		uni.setStorageSync('userInfo',res.userInfo);
				// 	},
				// 	fail: err => {
				// 		console.log(err.errMsg);
				// 	}
				// });
				// var _this = this;
				wx.showModal({
						title: '授权用于展示您的头像与微信昵称',
						content: '请点击按钮同意授权',
						success(res) {
							console.log(res)
							//如果用户点击了确定按钮
							if (res.confirm) {
								wx.getUserProfile({
									desc: '获取你的昵称、头像、地区及性别',
									success: res => {
										// _this.setData({
										// 	userInfo: res.userInfo,
										// 	hasUserInfo: true
										// })
										// 将获取的用户信息缓存到本地
										console.log(res);
										uni.setStorageSync('userInfo',res.userInfo);
										uni.setStorageSync('hasUserInfo',true);
									},
									fail: res => {
										console.log(res)
										//拒绝授权
										wx.showToast({
											title: '您拒绝了请求,授权失败',
											icon: 'error',
											duration: 2000
										});
										return;
									}
								});
							} else if (res.cancel) {
								//如果用户点击了取消按钮
								wx.showToast({
									title: '您拒绝了请求,授权失败',
									icon: 'error',
									duration: 2000
								});
								return;
							}
						}
					})
				}
			}
		}
</script>

<style lang="scss" scoped>
	.bg{
		width: 100%;
		height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		.advertising{
			position: fixed;
			bottom: 0;
		}
		
		button{
			margin-bottom: 75rpx;
			// width: 250rpx;
			// height: 100rpx;
			// border-radius: 10rpx;
			// background: linear-gradient(to right,#008FFF,#29C8FC);
			// color: #000000;
			line-height: 100rpx;
		}
		
		.bg-img{
			position: fixed;
			width: 100%;
			height: 100%;
		}
		
		.banner{
			position: fixed;
			top: 105rpx;
			width: 100%;
			height: 20%;
		}
		
		.tips{
			background: rgba(0,0,0,0.4);
			font-size: 32rpx;
			color: #FFF;
			position: absolute;
			bottom: 120rpx;
			z-index: 999;
			// width: 80%;
			border-radius: 20rpx;
			padding: 20rpx;
			margin-bottom: 60rpx;
		}
	}
</style>
