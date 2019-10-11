<template>
  <div class="details container">
    <!-- <router-link class="btn btn-default" to="/">返回</router-link> -->
    <button class="btn btn-default" @click="goback">返回</button>
    <h1 class="page-header">用户：{{ customer.name }}
        <span class="pull-right">
            <router-link class="btn btn-primary" :to="'/edit/' + id">编辑</router-link>
            <button class="btn btn-danger" @click="deleteCustomer( id )">删除</button>
        </span>
    </h1>
    <ul class="list-group">
        <li class="list-group-item"><span class="glyphicon glyphicon-phone">电话：  {{ customer.phone }}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-envelope">邮箱：  {{ customer.email }}</span></li>

        <li class="list-group-item"><span class="glyphicon glyphicon-thumbs-up">学历：  {{ customer.education }}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-thumbs-up">毕业学校：  {{ customer.graduationschool }}</span></li>

        <li class="list-group-item"><span class="glyphicon glyphicon-thumbs-up">职业：  {{ customer.profession }}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-thumbs-up">个人简介：  {{ customer.profile }}</span></li>
    </ul>
              
  </div>
</template>

<script>
export default {
  name: 'customersdetail',
  data () {
    return {
        customer:[],
        id: this.$route.params.id
    }
  },
  methods:{
      fetchCustomers(){
          this.$http.get( 'http://localhost:3000/users/' + this.id ).then( result =>{
              this.customer = result.body
          } )
      },
      deleteCustomer( id ){
          var flag= confirm('是否要删除该用户？');
                    if(flag){
                this.$http.delete( 'http://localhost:3000/users/' + id).then( result =>{
                this.$router.push({ path:'/',query:{alert: "用户信息删除成功！"} });
                    } );
                    }
           
      },
      goback(){
          this.$router.go(-1);
      }
      
  },
  created(){
      this.fetchCustomers();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
