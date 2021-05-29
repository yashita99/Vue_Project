<template>
  <div>
    <form>
      <div class="form-group" >
        <label for="id">Id</label>
        <input type="text" id="id" v-model="credentials.id"
		            name="id" class="form-control">
      </div>

      <div class="form-group" >
        <label for="name">Name</label>
        <input type="text" id="name" v-model="credentials.name"
		            name="name" class="form-control">
      </div>
			
      <div class="form-group">
        <label for="email">Email</label>
        <input type="email" v-model="credentials.email"
        id="email" class="form-control">
      </div>
      <div class="form-group">
        <label for="doc">Doc</label>
        <input type="doc" v-model="credentials.doc"
        id="doc" class="form-control">
      </div>
	    <b-btn type="submit" @click="updateUser()" class="btn  btn-md btn-block">UPDATE</b-btn>
    </form>
  </div> 
</template>

<script>
import Vue from 'vue'
import VueAxios from 'vue-axios'
import axios from 'axios'
Vue.use(VueAxios, axios)
export default {
  name: 'Edit',
  data () {
    return {
      credentials:
      {
        id: '',
        name: '',
        email: '',
        doc: ''
      }
    }
  },
  created: function () {
    this.getUsers(this.$route.params.id, this.$route.params.name, this.$route.params.email, this.$route.params.doc)
  },
  methods: {
    getUsers (_id, _name, _email, _doc) {
      // console.log(this.$router.data)
      // console.log(this.$route.params.id)
      // this.axios.get('http://localhost:4000/users').then((result) => {
      //   console.warn(result)
      this.credentials.id = _id
      this.credentials.name = _name
      this.credentials.email = _email
      this.credentials.doc = _doc
      // this.data()
    },
    updateUser () {
      // var body = [this.credentials.name, this.credentials.email]
      this.axios.put('http://localhost:4000/users/' + this.credentials.id, { name: this.credentials.name, email: this.credentials.email, doc: this.credentials.doc }).then((result) => {
        console.log(result)
        // console.log(this.credentials.name)
        // result.name = this.credentials.name
        // result.email = this.credentials.email
      })
      this.id = ''
      this.name = ''
      this.email = ''
      this.doc = ''
      this.$router.push('/')
    }
  }
}
</script>