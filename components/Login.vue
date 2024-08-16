<template>
  <div>
  <input 
    v-model="input.username"
    label="Full Name"
    placeholder="John Doe"
  >

  <input
      v-model="input.password"
      label="pass"
    placeholder="pass"
  >
  <!-- <div>
      <input type="text" v-model="input.username">
      <input type="text" v-model="input.password">

  </div> -->
  <p>{{  loginArea() }}</p>
  <button
    @click="login"
    :disable="!loginArea" 
  >
  login
  </button>
  </div>
</template>
<script>
export default{
    data(){
        return {
            input: {
                username: "",
                password: ""
            },
              loginMsg: ""

        }
    },
    methods:{
      loginArea() {
          if(this.input.username != "user") return false
          if(this.input.password != "pass") return false
          localStorage.setItem("user", "user")
          return true
      },
      login() {
          this.$router.push("/list") 
      }
    }
}
</script>