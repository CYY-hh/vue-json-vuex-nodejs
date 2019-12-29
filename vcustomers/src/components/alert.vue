<template>
  <div class="alter container">
 <div class="alert alert-warning alert-dismissible" role="alert">
   <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
   <strong></strong>  
   {{message}}
 </div>
  </div>
</template>

<script>
export default {
  name: 'alter',
  props:["message"],//绑定一个属性
  data () {
    return {
      
    }
  },
  // mounted() {
  // 	  this.$router.push({path:'/'})
  // }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 
</style>
