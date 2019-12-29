<template>
  <div class="customers container" ><!-- 设置显示的时候左右留白 -->
  <alert v-if="alert" :message="alert"></alert>
   <h1 class="page-header">用户管理系统</h1>
   <input type="text"  class="form-control" placeholder="搜索" v-model="filterinput" />
   <!-- class="form-control"是文本框变长，并有外观效果 -->
   <table class="table  table-striped">
	   <thead>
	   	<tr>
	   		<th>姓名</th>
	   		<th>电话</th>
	   		<th>邮箱</th>
			<th></th>
	   	</tr>
	   </thead>
	   <tbody>
	   	<tr  v-for="customer in search(filterinput)">
	   		<td>{{customer.name}}</td>
	   		<td>{{customer.phone}}</td>
	   		<td>{{customer.email}}</td>
	   		<td><router-link :to="'/customer/'+customer.id" class="btn btn-default">详情</router-link></td>
			<!-- :to="'/customer/'+customer.id" 使用v-bind绑定一个表达式 -->
	   	</tr>
	   </tbody>
   </table>
  </div>
</template>

<script>
import alert from './alert'//导入组件
export default {
  name: 'customers',
  data () {
    return {
		filterinput:"",
		alert:"",
      customers:[
		  
	  ]
    }
  },
  methods:{
	  fetchCustomers(){//这一步的实现需要安装路由vue-resource
		  this.$http.get("http://localhost:3000/users").then(function(response){
			  // console.log(response.body);
			  this.customers=response.body
		  })
	  },
	  search(filterinput){
		  return this.customers.filter(item =>{
			  if(item.name.includes(filterinput)){
				  return item
			  }
		  })
	  }
	  //item =>相当于function(item)
  },
  created() {
	  if(this.$route.query.alert){
		  this.alert=this.$route.query.alert
	  }
  	this.fetchCustomers();
  },
  updated() {
  	this.fetchCustomers()
  },
  components:{//添加组件
	  alert
  },
 mounted() {
 	  this.$router.push({path:'/'})//加上这个是首页的地址为原来的地址，否则无论刷新弹出也不会消失
 }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 
</style>
