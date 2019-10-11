<template>
  <div class="edit container">
    <button class="btn btn-default" @click="goback">返回</button>
    <h1 class="page-header">编辑用户：{{ customer.name }}</h1>
      <form @submit="editCustomer">
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
                  <button type="submit" class="btn btn-primary" >保存</button>
              </div>
          </div>
      </form>
  </div>
</template>

<script>
export default {
  name: 'edit',
  data () {
    return {
        customer:[],
        id: this.$route.params.id
    }
  },
  methods:{
        EditCustomer(){
            this.$http.get( 'http://localhost:3000/users/' + this.id ).then( result =>{
              this.customer = result.body
          } )
        },
        goback(){
          this.$router.go(-1);
        },
        editCustomer(e){
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
                this.$http.put( 'http://localhost:3000/users/' + this.id,Customers ).then( result =>{
                    this.$router.push({ path:'/',query:{alert: "用户信息更新成功！"} })
                    
                } )
                    e.preventDefault();  
            }
            e.preventDefault();
        }
  },
  created(){
      this.EditCustomer();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
