
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
const passwordRegex =
  /^(?=.*[A-Z])(?=.*[a-z])(?=.*\d)(?=.*[@#$%^&+=])[A-Za-z\d@#$%^&+=]{8,}$/;


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
this.PasswrdError = "";

if (!passwordRegex.test(this.password)) {
  this.PasswrdError =
    "Password must contain at least 8 characters, one uppercase letter, one lowercase letter, one number, and one special character.";
  return;
}

alert("Form submitted successfully!");

console.log({
  email: this.email,
  password: this.password,
  role: this.role,
  terms: this.terms,
  skills: this.skills,
});   
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
<style scoped>
.auth-wrapper {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #f4f6f8;
  font-family: Arial, sans-serif;
}

.card {
  width: 380px;
  background: white;
  padding: 30px;
  border-radius: 14px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.08);
}

h2 {
  margin-bottom: 5px;
}

.subtitle {
  font-size: 13px;
  color: #777;
  margin-bottom: 20px;
}

.field {
  margin-bottom: 15px;
}

label {
  display: block;
  font-size: 12px;
  margin-bottom: 5px;
  color: #555;
}

input, select {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 8px;
  outline: none;
  transition: 0.2s;
}

input:focus, select:focus {
  border-color: #4f46e5;
}

small {
  color: #e11d48;
  font-size: 12px;
}

button {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  background: #4f46e5;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: 0.2s;
}

button:hover {
  background: #4338ca;
}
</style>
