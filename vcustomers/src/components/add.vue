<template>
  <div class="add container">
	  <alert  v-if="alert" :message="alert"  ></alert>
	 <h1 class="page-header">添加用户</h1>
	<form @submit="addCustomer"><!-- 不在这里写也是可以出发的，但是是系统提供的，在这里写就是调用我们自己写的 -->
		<div class="well">
			<h4>用户信息</h4>
			<div class="form-group">
				<label>姓名：</label>
				<input type="text" class="form-control"  placeholder="name" v-model="customer.name"/>
			</div>
			<div class="form-group">
				<label>电话：</label>
				<input type="text" class="form-control"  placeholder="phone" v-model="customer.phone"/>
			</div>
			<div class="form-group">
				<label>邮箱：</label>
				<input type="text" class="form-control"  placeholder="email" v-model="customer.email"/>
			</div>
			<div class="form-group">
				<label>学历：</label>
				<input type="text" class="form-control"  placeholder="education" v-model="customer.education"/>
			</div>
			<div class="form-group">
				<label>毕业学校：</label>
				<input type="text" class="form-control"  placeholder="graduationschool" v-model="customer.graduationschool"/>
			</div>
			<div class="form-group">
				<label>职业：</label>
				<input type="text" class="form-control"  placeholder="profession" v-model="customer.profession"/>
			</div>
			<div class="form-group">
				<label>个人简介：</label>
				 <textarea rows="10" class="form-control" v-model="customer.profile"></textarea>
			</div>
			<button type="submit" class="btn btn-primary">添加</button>
		</div>
	</form>
  </div>
</template>

<script>
import alert from './alert'
export default {
  name: 'add',
  data () {
    return {
		alert:"",
      customer:{
		  
	  }
    }
  },
  methods:{
	  addCustomer(e){
		  if(!this.customer.name||!this.customer.phone||!this.customer.email){
			  this.alert="请添加相应信息"
		  }
		  else{
			  let newCustomer={
				  name:this.customer.name,
				  phone:this.customer.phone,
				  email:this.customer.email,
				  education:this.customer.education,
				  graduationschool:this.customer.graduationschool,
				  profession:this.customer.profession,
				  profile:this.customer.profile,
				  //id是自动添加的
			  }
			  this.$http.post("http://localhost:3000/users",newCustomer).then(function(response){
				  // console.log(response)
				  this.$router.push({path:"/",query:{alert:"用户信息添加成功！"}})
			  })
			   e.preventDefault()//这里有的时候不写会出错，这次是老师出错了
		  }
		  e.preventDefault()//阻止默认事件
	  }
  },
  components:{
	  alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 
</style>
