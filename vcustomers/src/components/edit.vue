<template>
  <div class="edit container">
	 <h1 class="page-header">编辑用户</h1>
	<form @submit="updateCustomer"><!-- 不在这里写也是可以出发的，但是是系统提供的，在这里写就是调用我们自己写的 -->
		<div class="well">
			<h4>用户信息</h4>
			<div class="form-group">
				<label>姓名：</label>
				<input type="text" class="form-control"  placeholder="name"  v-model="customer.name"/>
			</div>
			<div class="form-group">
				<label>电话：</label>
				<input type="text" class="form-control"  placeholder="phone"  v-model="customer.phone"/>
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
			<button type="submit" class="btn btn-primary">更新</button>
		</div>
	</form>
  </div>
</template>

<script>

	
export default {
  name: 'update',
  data () {
    return {
      customer:{
		  
	  }
    }
  },
  methods:{
	  updateCustomer(e){
		  if(!this.customer.name||!this.customer.phone||!this.customer.email){
			  console.log("请添加对信息")
		  }
		  else{
			  let updateCustomer={
				  name:this.customer.name,
				  phone:this.customer.phone,
				  email:this.customer.email,
				  education:this.customer.education,
				  graduationschool:this.customer.graduationschool,
				  profession:this.customer.profession,
				  profile:this.customer.profile,
				  //id是自动添加的
			  }
			  this.$http.put("http://localhost:3000/users/"+this.$route.params.id,updateCustomer).then(function(response){
				  // console.log(response)
				  
				  this.$router.push({path:"/",query:{alert:"用户信息更新成功！"}})
			  })
			   e.preventDefault()//这里有的时候不写会出错，这次是老师出错了
		  }
		  e.preventDefault()//阻止默认事件
	  }
  },
  created() {
  	this.$http.get("http://localhost:3000/users/"+this.$route.params.id).then(function(response){
  				  console.log(response.body);
  				  this.customer=response.body
  	})
	}
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 
</style>
