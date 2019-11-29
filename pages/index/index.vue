<template>
	<view class="container">
		<view class="top_mes">
		</view>
		<view class="section_list">
			<view class="left_list">
				<view class="list">
					<view class="admin_img">
						<image src="../../static/my_zl.png" mode="aspectFill"></image>
					</view>
					<text>admin用户</text>
				</view>
				<view class="list">
					<view class="zm_img">
						<image src="../../static/add.png" mode="aspectFill"></image>
					</view>
					<text>新增字幕</text>
				</view>
				<view class="list">
					<view class="cx_img">
						<image src="../../static/search.png" mode="aspectFill"></image>
					</view>
					<text>查询字幕</text>
				</view>
				<view class="list">
					<view class="up_img">
						<image src="../../static/update.png" mode="aspectFill"></image>
					</view>
					<text>更新字幕</text>
				</view>
				<view class="list">
					<view class="del_img">
						<image src="../../static/tel.png" mode="aspectFill"></image>
					</view>
					<text>删除字幕</text>
				</view>
				<view class="list">
					<view class="rw_img">
						<image src="../../static/rw.png" mode="aspectFill"></image>
					</view>
					<text>获取任务详情</text>
				</view>
				<view class="list">
					<view class="sh_img">
						<image src="../../static/sh.png" mode="aspectFill"></image>
					</view>
					<text>审核任务</text>
				</view>
				<view class="list">
					<view class="tx_img">
						<image src="../../static/tx.png" mode="aspectFill"></image>
					</view>
					<text>提现列表</text>
				</view>
				<view class="list">
					<view class="txsh_img">
						<image src="../../static/txsh.png" mode="aspectFill"></image>
					</view>
					<text>审核提现</text>
				</view>
			</view>
			<view class="right_list">
				<view class="add" v-if="id==0">
					<form @submit="tj" @reset="cz">
						<view class="file">
							<text>文件：</text>
							 <input type="text" value="" placeholder="" class="video"/> 
							<!-- <video :src="src" class="video"></video> -->
							<image src="../../static/wjj.png" mode="aspectFill"  @tap="chooseVideo" ></image>
						</view>
						<view class="sc">
							<text>时长：</text>
							<input type="text" value="" />
						</view>
						<view class="yx">
							<text>优先级：</text>
							<input type="text" value="" />
						</view>
						<view class="zm">
							<text>字幕：</text>
							<!-- <input type="text" value="" /> -->
							<textarea value="" maxlength="400" @blur="shiqu" @confirm="over"/>
						</view>
						<button form-type="submit" size="default">确认添加</button>
						
					</form>
				</view>
				<view class="search" v-else-if="id==1">
					<view class="cxzm">
						<text>搜索关键词 ：</text>
						<input type="text" >
					</view>
					<view class="uni-list">
					    <block v-for="(item,index) in lists" :key="index">
					        <view class="uni-list-cell" hover-class="uni-list-cell-hover">
					            <view class="uni-triplex-row">
					                <view class="uni-triplex-left">
					                    <text class="uni-title uni-ellipsis">34566543</text>
					                    <text class="uni-text">https://baidu.com</text>
					                    <text class="uni-text-small uni-ellipsis">两只老虎爱跳舞，小兔子乖乖拔萝卜，学习小鸭子走路，两只老虎爱跳舞，小兔子乖乖拔萝卜，学习小鸭子走路，</text>
					                </view>
					                <view class="uni-triplex-right">
					                    <text class="uni-h5">12:15</text>
					                </view>
					            </view>
					        </view>
					    </block>
					</view>
				</view>
				<view class="update" v-else-if="id==2">
					更新
				</view>
				<view class="dele" v-else-if="id==3">
					删除
				</view>
				<view class="detail" v-else-if="id==4">
					<view class="search_head">
					<text>搜索:</text>
					<input type="text" 
					placeholder="请输入搜索内容" 
					auto-focus="true"
					placeholder-style="color:#999"
					maxlength="200"
					cursor="10">
				</view>
				<view class="search_body">
					<view class="body_head">
						<view class="head_text" v-for="(list,index) in search_list" :key="index">
							<text>{{list.name}}</text>
						</view>
					</view>
					<view class="body_section"> 
						<view class="table" v-for="(listitem,index) in table" :key="index">
							 <view class="table_id">
								<text>{{listitem.id}}</text>
							</view>
							<view class="table_creatime">
								<text>{{listitem.createtime}}</text>
							</view>
							<view class="table_updattime">
								<text>{{listitem.update}}</text>
							</view>
							<view class="table_content">
								<text>{{listitem.content}}</text>
							</view>
							<view class="table_loca">
								<text>{{listitem.local}}</text>
							</view>
							<view class="table_audiotime">
								<text>{{listitem.audiotime}}</text>
							</view>
							<view class="table_yx">
								<text>{{listitem.priority}}</text>
							</view>
							<view class="table_status">
								<text>{{listitem.status}}</text>
							</view>
							<view class="table_detail">
								<text class="uni-icon uni-icon-compose"></text>
							</view>
						</view>
					</view>
				</view>
				</view>
				<view class="shenhe" v-else-if="id==5">
					<view class="sh">
						<view class="shtab">
							<view class="wsh" :current="current" v-for="sh in sh_list"  @clickItem="onClickItem">{{sh.name}}</view>
						</view>
						<view class="nr">
							<view v-show="current==0">
								<view class="rwsh">
									<view class="rw_head">
										
									</view>
								</view>
							</view>
							<view v-show="current==1">
								已审核
							</view>
							<view v-show="current==2">
								全部
							</view>
						</view>
					</view>
				</view>
				<view class="tx" v-else-if="id==5">
					提现列表
				</view>
				<view class="txsh" v-else-if="id==5">
					提现审核
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uniSegmentedControl from '@/components/uni-segmented-control/uni-segmented-control.vue'
	export default {
		components:{
				uniSegmentedControl
		},
		data() {
			return {
				left_list:[
					{id:0,name:'新增字幕'},
					{id:1,name:'查询字幕'},
					{id:2,name:'更新字幕'},
					{id:3,name:'删除字幕'},
					{id:4,name:'获取任务详情'},
					{id:5,name:'审核任务'},
					{id:6,name:'提现列表'},
					{id:7,name:'审核提现'}
				],
				id:0,
				search_list:[
					{name:'字幕id'},
					{name:'创建时间'},
					{name:'更新时间'},
					{name:'字幕文本'},
					{name:'音频地址'},
					{name:'音频时长'},
					{name:'优先级'},
					{name:'状态'},
					{name:'编辑'}
				],
				table:[
					{id:123,createtime:'2019-12-09',update:'2019-12-09',content:'123456...',local:'https://baidu.com',audiotime:'2000s',priority:'优先级',status:'状态'},
					{id:123,createtime:'2019-12-09',update:'2019-12-09',content:'123456...',local:'https://baidu.com',audiotime:'2000s',priority:'优先级',status:'状态'},
					{id:123,createtime:'2019-12-09',update:'2019-12-09',content:'123456...',local:'https://baidu.com',audiotime:'2000s',priority:'优先级',status:'状态'},
					{id:123,createtime:'2019-12-09',update:'2019-12-09',content:'123456...',local:'https://baidu.com',audiotime:'2000s',priority:'优先级',status:'状态'},
					{id:123,createtime:'2019-12-09',update:'2019-12-09',content:'123456...',local:'https://baidu.com',audiotime:'2000s',priority:'优先级',status:'状态'},
				],
				sh_list:[{name:'待审核'},{name:'未审核'},{name:'全部'}],
				current: 0,
				activeColor: '#007aff',
				styleType: 'button',
				list:[],
				src: ''
			}
		},
		onLoad() {
            let list = [];
            for (let i = 0; i < 5; i++) {
                list.push(i)
            }
            this.lists = list;
		},
		methods: {
			onClickItem(index) {
				if (this.current !== index) {
					this.current = index
				}
			},
			chooseVideo: function() {
				uni.chooseVideo({
					camera: this.cameraList[this.cameraIndex].value,
					sourceType: sourceType[this.sourceTypeIndex],
					success: (res) => {
						this.src = res.tempFilePath
					},
					fail: (err) => {
						// #ifdef MP
						uni.getSetting({
							success: (res) => {
								let authStatus = false;
								switch (this.sourceTypeIndex) {
									case 0:
										authStatus = res.authSetting['scope.camera'];
										break;
									case 1:
										authStatus = res.authSetting['scope.album'];
										break;
									case 2:
										authStatus = res.authSetting['scope.album'] && res.authSetting['scope.camera'];
										break;
									default:
										break;
								}
								if (!authStatus) {
									uni.showModal({
										title: '授权失败',
										content: 'Hello uni-app需要从您的相机或相册获取视频，请在设置界面打开相关权限',
										success: (res) => {
											if (res.confirm) {
												uni.openSetting()
											}
										}
									})
								}
							}
						})
						// #endif
					}
				})
			}
		}
		
	}
</script>

<style>
	.container{
		width:100%;height:1000px;
		border:1px solid #007AFF;
	}
	.top_mes{
		width:100%;height:80px;
		background-image: url('../../static/bg.jpg');
		background-size: cover;
		background-repeat: no-repeat;
		display: flex;
		flex-direction: row;
		align-items: center;
	}
	.section_list{
		width:100%;height:1800px;
		display: flex;
		flex-direction: row;
		border:1px solid #007AFF;
	}
	.left_list{
		width:15%;height:650px;
		background: #0A98D5;
		display: flex;
		justify-content: center;
		flex-direction: column;
		align-items: center;
	}
	.left_list .list{
		width:100%;height:80px;
		border-bottom:1px solid #fff;
		line-height: 65px;
		text-align: center;
		display: flex;
		justify-content: center;
		flex-direction: row;
	}
	.list view{
		width:30px;height:30px;
		margin-right: 10px;
	}
	.list view image{
		width:100%;height:100%;
		vertical-align:text-top ;
	}
	.list:hover{
		background: #007AFF;
		color:#D9D9D9;
	}
	.list text{
		display: inline-block;
		width:88px;height:60px;
		font-size: 14px;
	}
	.right_list{
		width:70%;height:700px;
		border:1px solid #007AFF;
	}
	.search_head{
		width:100%;height:20px;
		margin:  20px 30px;
		text-align: center;
		display: flex;
		flex-direction: row;
		
	}
	.search_head text{
		font-size: 14px;
	}
	.search_head input{
		border:1px solid #007AFF;
		border-radius: 15px;
		margin-left:20px;
	}
	.body_head,.body_section{
		width:100%;height:60px;
		display: flex;
		justify-content: space-between;
		flex-direction: row;
		border:1px solid #007AFF;
		text-align: center;
		margin-left:20px;
		background: #0A98D5;
		color:#D9D9D9;
	}
	.body_head .head_text,.table view{
		width:12%;height:60px;
		line-height: 16px;
		border-right: 1px solid #F1F1F1;
	}
	.body_head text{
		font-size: 14px;
	}
	.body_section{
		height: 600px;
		background: #FFFFFF;
		border:1px solid #007AFF;
		flex-direction: column;
	}
	.table{
		width:100%;height:60px;
		display: flex;
		justify-content: space-between;
		border-bottom:1px solid #F1F1F1;
		
	}
	.table view{
		overflow: hidden;
		text-overflow: ellipsis;
	}
	.table view text{
		font-size: 14px;
		color:#929292;
	}
	.file image{
		width:40px;height:40px;
	}
	.add{
		width:100%;height:600px;
		margin-left:20px;
		margin-top:20px;
	}
	.add form{
		width:100%;height:400px;
		display: flex;
		flex-direction: column;
		margin-top:80px;
		margin-left:120px;
	}
	form view{
		width:100%;height:60px;
		display: flex;
		flex-direction: row;
		align-items: center;
	}
	form view text{
		display: inline-block;
		width:60px;height:60px;
		line-height:60px;
		font-size: 14px;
	}
	form view input{
		width:300px;height:30px;
		border:1px solid #929292;
		border-radius:2px;
	}
	form button{
		width:30%;height:40px;
		line-height:40px;
		font-size: 13px;
		margin:10px 20px;
		background: #0A98D5;
		color:#F2F2F2;
	}
	form .zm{
		align-items: stretch;
		height:80px;
	}
	.zm textarea{
		width:300px;height:80px;
		border:1px solid #929292;
	}
	.shenhe{
		width:100%;height:600px;
		margin-left:40px;
		margin-top:40px;
	}
	.shenhe .sh .shtab{
		width:80%;height:60px;
		display: flex;
		justify-content: space-around;
		flex-direction: row;
		align-items: center;
		border:1px solid #B2B2B2;
	}
	.shtab view{
		width:35%;height:60px;
		line-height:60px;
		font-size: 14px;
		border-right: 1px solid #BEBEBE;
		text-align: center;
		color:#0A98D5
	}
	.cxzm{
		width:100%;height:60px;
		display: flex;
		flex-direction: row;
		margin-top:40px;
		margin-left:40px;
	}
	.cxzm text{
		font-size: 14px;
	}
	.cxzm input{
		border:1px solid #EEEEEE;
		width:180px;height:30px;
	}
	.uni-list-cell{
		width:100%;height:80px;
	}
	.uni-title {
		font-size: 17px;
		line-height:0.2
	}
	.uni-text{
		font-size: 15px;
	}
	.uni-text-small{
		font-size: 14px;
	}
	.uni-h5{
		font-size: 14px;
	}
</style>
