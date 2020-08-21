<template>
  <div class="customers container">
    <Alert :message="alert" v-if="alert"></Alert>
    <h1 page-header>用户管理系统</h1><br>
    <input type="text" class="form-control" v-model="searchKeywords" placeholder="搜索">
    <br>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>姓名</th>
          <th>电话</th>
          <th>邮箱</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="customer in keywords(customers,searchKeywords)" :key="customer.id">
          <td>{{customer.name}}</td>
          <td>{{customer.phone}}</td>
          <td>{{customer.email}}</td>
          <td><router-link class="btn btn-default" v-bind:to="'/Customer/'+customer.id">详情</router-link></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

import Alert from './Alert'

export default {
  name: 'Customers',
  data () {
    return {
      customers: [],
      alert: '',
      searchKeywords:''
    }
  },
  methods: {
    fetchCustomers () {
      this.$http.get('http://localhost:3000/users').then((response) => {
        this.customers = response.data
      })
    },
    keywords (customers,value) {
      return customers.filter(function(customer) {
        return customer.name.match(value);
      })
    }
  },
  created () {
    if(this.$route.query.alert) {
      this.alert = this.$route.query.alert;
    }
    this.fetchCustomers()
  },
  updated () {
    // this.fetchCustomers()
  },
  components:{
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
