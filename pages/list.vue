<template>

<v-row justify="center">
    <v-col
        cols="12"
        sm="10"
        md="8"
        lg="6"
    >
        <v-card ref="form">
            
            <v-card-text>
                <v-btn
                    color="primary"
                    variant="text"
                    @click="editUser"
                >
                {{ user }}</v-btn>
                でログインしたにゃ
            </v-card-text>
            <v-card-text>
                <v-text-field
                v-model="note"
                label="note"
                placeholder="投稿しよう"
                ></v-text-field>
            </v-card-text>
            <v-btn
                color="primary"
                variant="text"
                @click="notePost"
                :disable="!loginArea" 
            >
            投稿にゃ
            </v-btn>
            <v-card-text
                v-for="item in notes"
                v-bind:key="item">
                {{ item }}　by {{ user }}
            </v-card-text>
        </v-card>
    </v-col>
</v-row>

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