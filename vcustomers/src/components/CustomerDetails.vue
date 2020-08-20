<template>
  <div class="details container">
     <router-link class="btn btn-default" to="/">返回</router-link>
     <h1 class="page-header">
       {{customer.name}}
       <span class="pull-right">
          <router-link class="btn btn-primary text-right" v-bind:to="'/editor/'+customer.id">编辑</router-link>
          <button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">删除</button>
       </span>
       </h1>
     <ul class="list-group">
       <li class="list-group-item"><span class="glyphicon glyphicon glyphicon-phone"> {{customer.phone}}</span></li>
       <li class="list-group-item"><span class="glyphicon glyphicon-envelope"> {{customer.email}}</span></li>
     </ul>

     <ul class="list-group">
       <li class="list-group-item"><span class="glyphicon glyphicon-glass"> {{customer.educational}}</span></li>
       <li class="list-group-item"><span class="glyphicon glyphicon glyphicon-flag"> {{customer.graduationschool}}</span></li>
       <li class="list-group-item"><span class="glyphicon glyphicon glyphicon-briefcase"> {{customer.professional}}</span></li>
       <li class="list-group-item"><span class="glyphicon glyphicon glyphicon-user"> {{customer.profession}}</span></li>
     </ul>
  </div>
</template>

<script>
export default {
  name: 'customerdetails',
  data () {
    return {
      customer:''
    }
  },
  methods: {
    fetchCustomers (id) {
      this.$http.get('http://localhost:3000/users/'+id).then((response) => {
        this.customer = response.data
        // console.log(response.data)
      })
    },
    deleteCustomer (id) {
      // console.log(id);
      this.$http.delete('http://localhost:3000/users/'+id)
      .then((response) => {
         this.$router.push( {path: '/',query:{alert:'用户信息删除成功！'}} )
      })
    }
  },
  created () {
    this.fetchCustomers(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
   
</style>
