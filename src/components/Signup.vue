<template>
  <div :class="['auth-wrapper', darkMode ? 'dark' : 'light']">

    <button class="toggle" @click="darkMode = !darkMode">
      {{ darkMode ? '☀ Light Mode' : '🌙 Dark Mode' }}
    </button>

    <form class="card" @submit.prevent="handleSUbmit">

      <h2>Create Account</h2>

      <!-- Email -->
      <label>Email</label>
      <input v-model="email" type="email" />

      <!-- Password -->
      <label>Password</label>
      <input v-model="password" type="password" />

      <div v-if="PasswrdError" class="error">
        {{ PasswrdError }}
      </div>

      <!-- Role -->
      <label>Role</label>
      <select v-model="role">
        <option>Web Developer</option>
        <option>Web Designer</option>
      </select>

      <!-- Skills -->
      <label>Skills</label>

      <div class="skill-input">
        <input v-model="tempSkill" placeholder="Add skill" />
        <button type="button" @click="addskill">Add</button>
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

    removeskill(skill) {
      this.skills = this.skills.filter(s => s !== skill);
    },

    handleSUbmit() {
      this.PasswrdError = "";

      if (!passwordRegex.test(this.password)) {
        this.PasswrdError = "Weak password!";
        return;
      }

      alert("Success!");
    }
  }
};
</script>
<style scoped>
.auth-wrapper {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: 0.3s;
  font-family: Arial;
}

/* LIGHT */
.light {
  background: #f5f6fa;
}

/* DARK */
.dark {
  background: #0f172a;
}

.card {
  width: 380px;
  padding: 25px;
  border-radius: 16px;
  transition: 0.3s;
}

/* card light */
.light .card {
  background: white;
  color: black;
}

/* card dark */
.dark .card {
  background: #1e293b;
  color: white;
}

label {
  display: block;
  margin-top: 10px;
  font-size: 12px;
}

input, select {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  border-radius: 8px;
  border: 1px solid #ccc;
}

.dark input,
.dark select {
  background: #0f172a;
  color: white;
  border: 1px solid #334155;
}

.skill-input {
  display: flex;
  gap: 10px;
}

.skill-input button {
  background: #6366f1;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 8px;
  cursor: pointer;
}

.skills {
  margin-top: 10px;
}

.skills span {
  display: inline-block;
  background: #6366f1;
  color: white;
  padding: 5px 10px;
  margin: 3px;
  border-radius: 20px;
  cursor: pointer;
  font-size: 12px;
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
}

.error {
  color: #f87171;
  font-size: 12px;
  margin-top: 5px;
}

.toggle {
  position: absolute;
  top: 20px;
  right: 20px;
  padding: 8px 12px;
  border-radius: 8px;
  border: none;
  cursor: pointer;
}
</style>
