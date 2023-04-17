<template>
<div class="container">
    <h1>Name : {{name}}</h1>
    <h1>Email : {{email}}</h1>
    <h1>DOB : {{dob}}</h1>

    <img :src="imageUrl" alt="Profile Picture" /> <br>
    <button @click="calculateAge">Calculate Age</button>
    <p>Your age is : {{age}}</p>
    <button v-on:click="validateAge">Validate Age</button>
    <div v-if="showResults">
        <p v-if="age !== null">
          <span class="error" v-if= "age < 18">You are underage.</span>
          <span class="right" v-else>You are ok to use this website.</span>
        </p>
    </div>

    <ul>
        <li v-for="item in users" :key="item.name">
           {UserName is {{item.name}} and Age : {{item.age}} } 
        </li>
    </ul>

</div>
</template>

<script>
export default {
    data(){
        return{
            name : "Sakshi Gupta",
            email : "sakshhi@gmail.com",
            dob : "02/08/2001",
            age : null,
            showResults : false,
            imageUrl : "https://tse2.mm.bing.net/th?id=OIP.oqmBe8wpnsCUUuxUwyv5TAHaE8&pid=Api&P=0",
            users : [{
                name : "rahul",
                age : "20"
            },
            {
                name : "anil",
                age  : "21"
            }],
        }
    },
    methods: {
        calculateAge: function() {
            const dob  = new Date(this.dob);
            const now = new Date();
            const diffInMilliseconds = now - dob.getTime();
            const ageDate = new Date(diffInMilliseconds);
            const age = Math.abs(ageDate.getUTCFullYear() -1970);
            this.age = age;
        },
        validateAge: function() {
            this.showResults = true;
            if(this.age<18){
                this.underAge = true;
            }
            else{
                this.underAge = false;
            }
        }
    }
}
</script>

<style scoped>
.error{
    color: red;
}
.right{
    color: green;
}
</style>
