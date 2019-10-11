<template>
  <div class="add container">
      <h1 class="page-header">添加用户</h1>
      <form @submit="addCustomer">
          <div class="well">
              <h4>用户信息</h4>
              <div class="form-group">
                  <label><span style="color:red">* </span>姓名</label>
                  <input type="text" class="form-control" placeholder="name" v-model="customer.name">
                  <label><span style="color:red">* </span>电话</label>
                  <input type="text" class="form-control" placeholder="phone" v-model="customer.phone" oninput="value=value.replace(/[^\d]/g,'')">
                  <label><span style="color:red">* </span>邮箱</label>
                  <input type="email" class="form-control" placeholder="email" v-model="customer.email">
                  <label>学历</label>
                  <input type="text" class="form-control" placeholder="education" v-model="customer.education">
                  <label>毕业学校</label>
                  <input type="text" class="form-control" placeholder="graduationschool" v-model="customer.graduationschool">
                  <label>职业</label>
                  <input type="text" class="form-control" placeholder="profession" v-model="customer.profession">
                  <label>个人简介</label>
                  <!-- <input type="text" class="form-control" placeholder="name" v-model="customer.profile"> -->
                  <textarea class="form-control" placeholder="" rows="10" v-model="customer.profile" ></textarea>
                  <button type="submit" class="btn btn-primary" >添加</button>
              </div>
          </div>
      </form>
  </div>
</template>

<script>
export default {
  name: 'add',
  data () {
    return {
        customer:{}
    }
  },
  methods:{
        addCustomer(e){
            if( !this.customer.name || !this.customer.phone || !this.customer.email ){
                alert('* 内容为必填信息！');              
            }
            else{
                var Customers = {
                    name: this.customer.name,
                    phone: this.customer.phone,
                    email: this.customer.email,
                    education: this.customer.education,
                    graduationschool: this.customer.graduationschool,
                    profession: this.customer.profession,
                    profile: this.customer.profile,
                }
                this.$http.post( 'http://localhost:3000/users',Customers ).then( result =>{
                    this.$router.push({ path:'/',query:{alert: "用户信息添加成功！"} })
                    
                } )
                    e.preventDefault();  
            }
            e.preventDefault();
  }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
