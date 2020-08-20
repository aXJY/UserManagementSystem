<template>
  <div class="editor container">
    <Alert v-if="alert" v-bind:message="alert"></Alert>
    <h1 class="page-header">编辑用户</h1>
    <form v-on:submit="updatepCustomer">
        <div class="well">
            <h4>用户信息</h4>
            <div class="form-group">
                <label>姓名</label>
                <input type="text" class="form-control" placeholder="name" v-model="customer.name">
            </div>
            <div class="form-group">
                <label>电话</label>
                <input type="text" class="form-control" placeholder="phone" v-model="customer.phone">
            </div>
            <div class="form-group">
                <label>邮箱</label>
                <input type="text" class="form-control" placeholder="email" v-model="customer.email">
            </div>
            <div class="form-group">
                <label>学历</label>
                <input type="text" class="form-control" placeholder="educational" v-model="customer.educational">
            </div>
            <div class="form-group">
                <label>毕业学校</label>
                <input type="text" class="form-control" placeholder="graduationschool" v-model="customer.graduationschool">
            </div>
            <div class="form-group">
                <label>职业</label>
                <input type="text" class="form-control" placeholder="professional" v-model="customer.professional">
            </div>
            <div class="form-group">
                <label>个人简介</label>
                <textarea class="form-control" v-model="customer.profession" rows="10"></textarea>
            </div>
            <button type="submit" class="btn btn-primary">确认</button>
        </div>
    </form>
  </div>
</template>

<script>
import Alert from './Alert'
export default {
  name: 'editor',
  data () {
    return {
        customer: {},
        alert:''
    }
  },
  methods:{
      fetchCustomer(id) {
        this.$http.get('http://localhost:3000/users/'+id)
        .then((response) => {
            this.customer=response.data;
        })
      },
     updatepCustomer(e){
       if(!this.customer.name || !this.customer.phone || !this.customer.email) {
           this.alert="请添加相应信息！";
       } else {
           let updatepCustomer = {
               name:this.customer.name,
               phone:this.customer.phone,
               email:this.customer.email,
               educational:this.customer.educational,
               graduationschool:this.customer.graduationschool,
               professional:this.customer.professional,
               profession:this.customer.profession
           }
           this.$http.put('http://localhost:3000/users/'+this.$route.params.id,updatepCustomer)
           .then((response) => {
               this.$router.push({path:'/',query:{alert:'用户信息更新成功！'}});
               console.log(response.data)
           })
        e.preventDefault();
       }
       e.preventDefault();
     }
  },
  created () {
    this.fetchCustomer(this.$route.params.id);
  },
  components:{
      Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>