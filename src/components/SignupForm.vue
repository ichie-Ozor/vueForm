<template>
<div class="form">
  <form @submit.prevent="onsubmitHandler">
    <label>Email:</label>
    <input type="email" required v-model="email"/>

    <label>Password</label>
    <input type="password" required v-model="password">
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
        <option value="devops">DevOps</option>
        <option value="dataAnalyst">Data Analyst</option>
        <option value="cyberSecurity">Cyber Security</option>
        <option value="techWriter">Technical Writer</option>
    </select>
    <div class="terms">
        <input type="checkbox" v-model="terms"/>
        <label>Accept terms and conditions</label>
    </div>

    <label>Skills</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill">
    <div class="pills" v-for="skill in skills" :key="skill">
        <span @click="deleteSkill(skill)">{{skill}}</span>
    </div>
    <div class="submit">
    <button>Create An Account</button>
  </div>
  </form>
  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{role}}</p>
  <p>Terms accpted: {{terms }}</p>
  </div>
</template>

<script>
export default {
  data(){
    return {
        email: '',
        password: '',
        role: '',
        terms: false,
        tempSkill: '',
        skills: [],
        passwordError: ''
    }
  },
  methods: {
    addSkill(e){
        console.log(e)
        if(e.key === 'Enter' && this.tempSkill){
            if(!this.skills.includes(this.tempSkill)){
                this.skills.push(this.tempSkill)
            }
            this.tempSkill = ''
        }
    },
    deleteSkill(skill){
        this.skills = this.skills.filter((item) => {
            return skill !== item
        })
    },
    onsubmitHandler(){
        console.log("form submitted")
        // validate password
        this.passwordError = this.password.length > 5 ?
        '' :
        'password must be at least 6 chars long'

        if(!this.passwordError){
            console.log('email', this.email)
            console.log('password', this.password)
            console.log('role', this.role)
            console.log('skill', this.tempSkill)
            console.log('terms', this.terms)
        }
    }
  }
}
</script>

<style>
.form{
    max-width: 550px;
    margin: 30px auto;
    background: rgb(172, 73, 73);
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
form{
    max-width: 420px;
    margin: 30px auto;
    background: rgb(233, 218, 218);
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input[type="checkbox"]{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.pills{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    font-size: 15px;
    font-weight: 600;
}
.submit{
    text-align: center;
}
.error{
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>