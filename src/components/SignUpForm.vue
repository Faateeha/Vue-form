<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email">
    <label>Password:</label>
    <input type="password" required v-model="password">
    <div v-if="passwordError" class="error">{{ passwordError }}</div>
    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill">
    <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>
    <div class="terms">
        <input type="checkbox" v-model="terms" required>
        <label>I agree to the terms and conditions</label>  
    </div>

    <div class="buuton">
        <button>Create an Account</button>
    </div>
  </form>
  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Accepted: {{ terms }}</p>
</template>

<script>
export default {
    data(){
        return {
            email: '',
            password: '',
            role: 'developer',
            terms: false,
            tempSkill: '',
            skills: [],
            passwordError: ''
        }
    
    },
    methods: {
        addSkill(e) {
            if(e.key === ',' && this.tempSkill) {
                if(!this.skills.includes(this.tempSkill)) {
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
        handleSubmit(){
            //validate password
            this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 characters'

            if(!this.passwordError) {
                console.log('email:', this.email)
                console.log('password:', this.password)
                console.log('role:', this.role)
                console.log('skills:', this.skills)
                console.log('terms:', this.terms)
            }
        }
    }
}
</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    padding: 40px;
    text-align: left;
    background: white;
    border-radius: 10px;
    
}
label {
    display: inline-block;
    color: #aaa;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select {
    width: 100%;
    display: block;
    padding: 10px 6px;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.pill {
    display: inline-block;
    background: #eee;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    padding: 6px 12px;
    margin: 20px 10px 0 0;
    border-radius: 20px;
    cursor: pointer;
}
button {
    background: #0b6dff;
    color: white;
    padding: 10px 20px;
    border: 0;
    border-radius: 20px;
    cursor: pointer;
    margin-top: 20px;
}
.submit{
    text-align: center;
}
.error {
    color: #ff0062;
    font-weight: bold;
    font-size: 0.8em;
    margin-top: 10px;
}
</style>