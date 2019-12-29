<template>
  <div class="detail container">
	  <router-link to="/" class="btn btn-default">返回</router-link>
 <h1 class="page-header">{{customers.name}}
 <span class="pull-right">
	 <router-link class="btn btn-primary" v-bind:to="'/edit/'+customers.id"><!-- 要命的少了个s -->
		 编辑
	 </router-link>
	 <button class="btn btn-danger" @click="deleteCustomer(customers.id)">删除</button>
 </span><!-- 实在当前的最右侧 -->
 </h1>
 <ul class="list-group">
 	<li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customers.phone}}</span></li>
 	<li class="list-group-item"><span class="glyphicon glyphicon-cloud">{{customers.email}}</span></li>
 </ul>
 
 <ul class="list-group">
 	<li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customers.education}}</span></li>
 	<li class="list-group-item"><span class="glyphicon glyphicon-cloud">{{customers.graduationschool}}</span></li>
	<li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customers.profession}}</span></li>
	<li class="list-group-item"><span class="glyphicon glyphicon-cloud">{{customers.profile}}</span></li>
 </ul>
  </div>
</template>


<script>
export default {
  name: 'customerdetails',
  data () {
    return {
      customers:[]
    }
  },
  methods:{
	  deleteCustomer(id){
		  // console.log(id)
		  this.$http.delete("http://localhost:3000/users/"+id).then(function(response){
			  this.$router.push({path:'/',query:{alert:"用户删除成功"}})
		  })
	  },
	  fetchCustomers(id){//这一步的实现需要安装路由vue-resource
	  		  this.$http.get("http://localhost:3000/users/"+id).then(function(response){
	  			  // console.log(response.body);
	  			  this.customers=response.body
	  		  })
	  }
  },
  created() {
  	this.fetchCustomers(this.$route.params.id)//从customer中点击的时候传过来的id值
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 
</style>
