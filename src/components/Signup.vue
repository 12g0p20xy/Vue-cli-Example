<template>

	<div class="signup">
		<button class="btn btn-danger" @click="open()">弹出一个登录框:)</button>
		<div class="layer" :class="{active: show}">
			<div class="signup-box">
				<div class="input-group">
			      <label for="">姓名:</label>
			      <input type="text" class="form-control" placeholder="姓名">
			    </div>
			    <div class="input-group">
			      <label for="">邮箱:</label>
			      <input type="mail" class="form-control" placeholder="邮箱">
			    </div>
			    <div class="input-group">
			      <label for="">密码:</label>
			      <input type="password" class="form-control" v-model="password" @keyup="passwordRank()" placeholder="密码">
			    </div>
			    <div>
				    <b>密码强度：{{ strong }}</b>
				    <div class="line">
				    	<i :class="{ active: rank1 }"></i>
				    	<i :class="{ active: rank2 }"></i>
				    	<i :class="{ active: rank3 }"></i>
				    	<i :class="{ active: rank4 }"></i>
				    </div>
				   </div>
			    <input type="button" class="btn btn-success" value="注册">
			    <a class="close-btn" href="javascript:;" @click="open">取消</a>
		    </div>
		</div>
	</div>
	
</template>

<script>
export default {
	data () {
		return {
			show: false,   // 是否显示登录框
			password: '',  // 输入的密码
			rank1: false,	 // 密码强度等级
			rank2: false,
			rank3: false,
			rank4: false
		}
	},
	computed: {
		// 计算密码强度的规则
		strong () {
			let strong = 0
      if (this.password.length < 4) return 0
      if (/\d/.test(this.password)) strong++
      if (/[a-z]/.test(this.password)) strong++
      if (/[A-Z]/.test(this.password)) strong++
      if (/\W/.test(this.password)) strong++
      if (this.password.length > 10) return 4
      return strong
		}
	},
  methods: {
    open () {
    	this.show = !this.show
    	return this.show
    },
    checkOut (value) {
    	console.log(value)
    },
    passwordRank () {
    	switch (this.strong) {
    		case 0:
    			this.rank1 = false
    			this.rank2 = false
    			this.rank3 = false
    			this.rank4 = false
    			break
    		case 1:
    			this.rank1 = true
    			this.rank2 = false
    			this.rank3 = false
    			this.rank4 = false
    			break
    		case 2:
    			this.rank1 = true
    			this.rank2 = true
    			this.rank3 = false
    			this.rank4 = false
    			break
    		case 3:
    			this.rank1 = true
    			this.rank2 = true
    			this.rank3 = true
    			this.rank4 = false
    			break
    		case 4:
    			this.rank1 = true
    			this.rank2 = true
    			this.rank3 = true
    			this.rank4 = true
    			break
    	}
    }
  }
}
</script>

<style lang="less" scoped>
	.layer{
		display: none;
		position: fixed;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		background: rgba(255,255,255,.8);
		z-index: 99;
		&.active{
			display: block;
			.signup-box{
				animation: show .3s forwards;
			}
		}
		.signup-box{
			position: absolute;
			top: 50%;
			left: 50%;
			padding: 30px;
			border: 1px solid #ddd;
			background: #fff;
			box-shadow: 0 6px 30px #ccc;
			transform: translate(-50%, -50%) scale(5);
			opacity: 0;
			.input-group{
				margin-bottom: 1em;
				label{
					display: block;
				}
				input{
					width: 15em;
				}
			}
			.line{
				display: block;
				width: 100%;
				margin: .5em 0;
				i{
					display: block;
					float: left;
					width: 25%;
					height: 8px;
					border-right: 2px solid #fff;
					background: #eee;
					margin-bottom: 1em;
					&:nth-child(1).active{
						background: lighten(yellowgreen, 20%)
					}
					&:nth-child(2).active{
						background: lighten(yellowgreen, 10%)
					}
					&:nth-child(3).active{
						background: yellowgreen
					}
					&:nth-child(4).active{
						background: darken(yellowgreen, 10%)
					}
				}
			}
			.close-btn{
				margin-left: 1em;
			}
		}
	}
	@keyframes show{
		to {
			transform: translate(-50%, -50%) scale(1);
			opacity: 1;
		}
	}
</style>
