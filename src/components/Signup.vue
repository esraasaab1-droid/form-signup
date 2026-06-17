
  <template>
    <link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/css/all.min.css"
/>
  <form @submit.prevent="handleSUbmit">
    
    <label>
      <i class="fa-solid fa-envelope"></i>
      Email:
    </label>
    <input v-model="email" type="email" required />

    <label>
      <i class="fa-solid fa-lock"></i>
      Password:
    </label>
    <input v-model="password" type="password" required />

    <div v-if="PasswrdError" class="error">
      <i class="fa-solid fa-triangle-exclamation"></i>
      {{ PasswrdError }}
    </div>

    <label>
      <i class="fa-solid fa-user-tie"></i>
      Role:
    </label>
    <select v-model="role" required>
      <option value="developer">Web Developer</option>
      <option value="Designer">Web Designer</option>
    </select>

    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label>
        <i class="fa-solid fa-circle-check"></i>
        I agree to the terms and conditions
      </label>
    </div>

    <label>
      <i class="fa-solid fa-code"></i>
      Skills:
    </label>
    <input
      type="text"
      v-model="tempSkill"
      required
      @keyup.space="addskill"
    />

    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="removeskill(skill)">
        <i class="fa-solid fa-gem"></i>
        {{ skill }}
      </span>
    </div>

    <div class="submit">
      <button>
        <i class="fa-solid fa-user-plus"></i>
        Create an Account
      </button>
    </div>

  </form>
</template>

<script>
import Signup from "./Signup.vue";
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      skills: [],
      PasswrdError:''
    };
  },
  methods: {
    addskill(e) {
      if (e.key === " " && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    removeskill(skill) {
      this.skills = this.skills.filter((s) => {
        return skill !== s;
      });
    },
    handleSUbmit(){
        this.PasswrdError=this.password.length < 8 ? 'Password must be at least 8 characters long':'';
   
   if(!this.PasswrdError){
    alert('Form submitted successfully!');
    console.log({
      email: this.email,
      password: this.password,
      role: this.role,
      terms: this.terms,
      skills: this.skills
    });
   }
  }
}}
</script>
<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  box-sizing: border-box;
  display: block;
  width: 100%;
  padding: 10px 6px;
  font-size: 1.2em;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 3px;
  border-radius: 2px solid black;
}
.pill {
  display: inline-block;
  top: 2px;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background-color: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
  width: 16px;
}
button {
  background-color: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  border-radius: 20px;
  color: white;
}

.submit {
  text-align: center;
}
.error{
    color: rgb(198, 48, 48);
    font-size: 0.8em;
    margin-top: 10px;
    font-weight: bold;
   
    font-family: Arial, Helvetica, sans-serif;
}
i {
  margin-right: 6px;
}

button i {
  margin-right: 8px;
}

.error i {
  margin-right: 5px;
}
</style>