<template>
    <div>
    <button
        color="primary"
        variant="text"
        @click="editUser"
    >
    {{ user }}</button>
    <p>{{ user }}でログインしたにゃ</p>
    <input
        v-model="note"
        label="note"
        placeholder="投稿しよう"
    >
    <button
        color="primary"
        variant="text"
        @click="notePost"
        :disable="!loginArea" 
    >
    投稿にゃ
    </button>
    <p v-for="item in notes"
        v-bind:key="item">
        {{ item }}　by {{ user }}
    </p>
</div>
</template>

<script>
export default{
    data(){
        return {
            note: "",
            notes: [],
            user: ""
        }
    },
    methods:{
        notePost() {
            console.log(this.note)
            console.log(this.notes)
            this.notes.push(this.note)
            localStorage.setItem("notes", JSON.stringify(this.notes))
            console.log(localStorage.getItem("notes"))
            this.note = ""
        },
        editUser() {
            this.$router.push("/user/editUser") 
        }
    },
    mounted() {
        if(!localStorage.getItem("user")) {
            this.$router.push("/") 
        }else{
            this.user = localStorage.getItem("user")
        }
    }
}
</script>