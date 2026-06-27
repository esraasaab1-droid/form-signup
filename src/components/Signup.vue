<template>
  <div :class="['auth-wrapper', darkMode ? 'dark' : 'light']">

    <!-- Theme Icon -->
    <div class="theme-icon" @click="toggleTheme">
  <i :class="darkMode ? 'fa-solid fa-sun' : 'fa-solid fa-moon'"></i>
</div>
    <form class="card" @submit.prevent="handleSUbmit">

      <h2>Create Account</h2>

      <!-- Email -->
      <label>Email</label>
      <input v-model="email" type="email" required />

      <!-- Password -->
      <label>Password</label>
<input v-model="password" type="password" @input="PasswrdError = ''" />
      <div v-if="PasswrdError" class="error">
        {{ PasswrdError }}
      </div>

      <!-- Role -->
      <label>Role</label>
      <select v-model="role" required>
        <option>Web Developer</option>
        <option>Web Designer</option>
      </select>

      <!-- Skills -->
      <label>Skills</label>

      <div class="skill-input">
<input v-model="tempSkill" @input="skillsError = ''" placeholder="Add skill" />
        <button type="button" @click="addskill">
          Add
        </button>
      </div>

      <div v-if="skillsError" class="error">
        {{ skillsError }}
      </div>

      <div class="skills">
        <span v-for="s in skills" :key="s" @click="removeskill(s)">
          {{ s }} ✕
        </span>
      </div>

      <!-- Submit -->
      <button class="submit-btn" type="submit">
        Create Account
      </button>

    </form>
  </div>
</template>
<script>
const passwordRegex =
  /^(?=.*[A-Z])(?=.*[a-z])(?=.*\d)(?=.*[@#$%^&+=])[A-Za-z\d@#$%^&+=]{8,}$/;

export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      skills: [],
      tempSkill: "",
      PasswrdError: "",
      skillsError: "",
    darkMode: false
    };
  },

  methods: {
    addskill() {
      if (this.tempSkill && !this.skills.includes(this.tempSkill)) {
        this.skills.push(this.tempSkill);
      }
      this.tempSkill = "";
    },
     toggleTheme() {
    this.darkMode = !this.darkMode;
  }
,
    removeskill(skill) {
      this.skills = this.skills.filter(s => s !== skill);
    },

  handleSUbmit() {
  this.PasswrdError = "";
  this.skillsError = "";

  let hasError = false;

  // password check
  if (!passwordRegex.test(this.password)) {
    this.PasswrdError =
      "Password must include uppercase, lowercase, number, and symbol";
    hasError = true;
  }

  // skills check
  if (this.skills.length === 0) {
    this.skillsError = "Please add at least one skill";
    hasError = true;
  }

  // stop only if errors exist
  if (hasError) return;

  // success
  alert("Account created successfully!");

  console.log({
    email: this.email,
    password: this.password,
    role: this.role,
    skills: this.skills
  });

  // reset
  this.email = "";
  this.password = "";
  this.role = "";
  this.skills = [];
  this.tempSkill = "";
}
  }
};
</script>
<style scoped>
.auth-wrapper {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: 0.3s;
  font-family: Arial, sans-serif;
  padding: 20px;
}


.light {
  background: #f4f6f8;
  color: #111;
}

.light .card {
  background: #ffffff;
}

 
.dark {
  background: #0f172a;
  color: #f8fafc;
}

.dark .card {
  background: #1e293b;
}

 
.card {
  width: 380px;
  padding: 25px;
  border-radius: 14px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.08);
  transition: 0.3s;
}

 
input,
select {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  border-radius: 8px;
  border: 1px solid #ccc;
  outline: none;
  transition: 0.2s;
  font-size: 14px;
}

input:focus,
select:focus {
  border-color: #4f46e5;
}

/* dark inputs */
.dark input,
.dark select {
  background: #0f172a;
  color: white;
  border: 1px solid #334155;
}

 
label {
  display: block;
  margin-top: 12px;
  font-size: 12px;
  font-weight: bold;
  opacity: 0.8;
}

 
.error {
  color: #f87171;
  font-size: 12px;
  margin-top: 5px;
}

 
.skill-input {
  display: flex;
  gap: 10px;
  margin-top: 5px;
}

.skill-input button {
  background: #4f46e5;
  color: white;
  border: none;
  padding: 10px 14px;
  border-radius: 8px;
  cursor: pointer;
  transition: 0.2s;
}

.skill-input button:hover {
  background: #4338ca;
  transform: translateY(-1px);
}

 
.skills {
  margin-top: 10px;
}

.skills span {
  display: inline-block;
  background: #4f46e5;
  color: white;
  padding: 5px 10px;
  margin: 4px;
  border-radius: 20px;
  font-size: 12px;
  cursor: pointer;
  transition: 0.2s;
}

.skills span:hover {
  background: #4338ca;
  transform: scale(1.05);
}

 
.submit-btn {
  width: 100%;
  margin-top: 15px;
  padding: 10px;
  border: none;
  border-radius: 8px;
  background: #22c55e;
  color: white;
  cursor: pointer;
  transition: 0.2s;
}

.submit-btn:hover {
  background: #16a34a;
  transform: translateY(-1px);
}

 
.theme-icon {
  position: fixed;
  top: 18px;
  right: 18px;
  font-size: 22px;
  cursor: pointer;
  z-index: 9999;

  background: none;
  width: auto;
  height: auto;
  padding: 0;

  transition: 0.2s;
}

.theme-icon:hover {
  transform: scale(1.2);
}

 .light .theme-icon {
  color: #111;
}

.dark .theme-icon {
  color: #facc15;
}
</style>
