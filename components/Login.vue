<template>
  <div>
  <input 
    v-model="input.user"
    label="Full Name"
    placeholder="user"
  >

  <!-- <input
      v-model="input.password"
      label="pass"
    placeholder="pass"
  > -->
  <!-- <div>
      <input type="text" v-model="input.username">
      <input type="text" v-model="input.password">

  </div> -->
  <!-- <p>{{  loginArea() }}</p> -->
  <button
    @click="login">
    <!-- :disable="!loginArea"  -->
  <!-- > -->
  login
  </button>
  </div>
</template>
<script>
export default{
    data(){
        return {
            input: {
                user: "",
                // password: ""
            },
            loginMsg: "",

            colors: ['#FF5733', '#33FF57', '#3357FF', '#FF33A6', '#A633FF', '#33FFF5'], // 色のリスト
            randomColor: '', // ランダムに選ばれた色を格納する変数

        }
    },
    methods:{
      // loginArea() {
      //     if(this.input.username != "user") return false
      //     if(this.input.password != "pass") return false
      //     localStorage.setItem("user", "user")
      //     return true
      // },
      login() {
        this.getRandomColor();
        localStorage.setItem("user", this.input.user)
        localStorage.setItem("color", this.randomColor)
        this.$router.push("/drawing") 
      },
      getRandomColor() {
        // 色のリストからランダムに1つを選択
        const randomIndex = Math.floor(Math.random() * this.colors.length);
        this.randomColor = this.colors[randomIndex];
      },
    }
}
</script>