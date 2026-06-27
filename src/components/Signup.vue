<template>
  <div :class="['auth-wrapper', darkMode ? 'dark' : 'light']">

    <!-- Theme Icon -->
    <div class="theme-icon" @click="darkMode = !darkMode">
      <i :class="darkMode ? 'fa-solid fa-sun' : 'fa-solid fa-moon'"></i>
    </div>

    <form class="card" @submit.prevent="handleSUbmit">

      <h2>Create Account</h2>

      <!-- Email -->
      <label>Email</label>
      <input v-model="email" type="email" required />

      <!-- Password -->
      <label>Password</label>
      <input v-model="password" type="password" required />

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
        <input v-model="tempSkill" placeholder="Add skill" />
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

    removeskill(skill) {
      this.skills = this.skills.filter(s => s !== skill);
    },

    handleSUbmit() {
      this.PasswrdError = "";
      this.skillsError = "";

      // Password validation (شرح واضح)
      if (!passwordRegex.test(this.password)) {
        this.PasswrdError =
          "Password must be 8+ characters and include: uppercase, lowercase, number, and special symbol (@#$%^&+=)";
        return;
      }

      // Skills validation
      if (this.skills.length === 0) {
        this.skillsError = "Please add at least one skill";
        return;
      }

      alert("Account created successfully!");

      console.log({
        email: this.email,
        password: this.password,
        role: this.role,
        skills: this.skills
      });
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
  font-family: Arial;
}

/* LIGHT */
.light {
  background: #f4f6f8;
  color: #111;
}

/* DARK */
.dark {
  background: #0f172a;
  color: #fff;
}

.card {
  width: 380px;
  padding: 25px;
  border-radius: 14px;
  transition: 0.3s;
}

.light .card {
  background: white;
}

.dark .card {
  background: #1e293b;
}

/* Inputs */
input, select {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  border-radius: 8px;
  border: 1px solid #ccc;
}

/* Dark inputs */
.dark input,
.dark select {
  background: #0f172a;
  color: white;
  border: 1px solid #334155;
}

/* Skill input */
.skill-input {
  display: flex;
  gap: 10px;
  margin-bottom: 10px;
}

.skill-input button {
  background: #4f46e5;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 8px;
  cursor: pointer;
}

/* Skills */
.skills span {
  display: inline-block;
  background: #4f46e5;
  color: white;
  padding: 5px 10px;
  margin: 4px;
  border-radius: 20px;
  cursor: pointer;
  font-size: 12px;
}

/* Submit */
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

/* Error */
.error {
  color: #f87171;
  font-size: 12px;
  margin-top: 5px;
}

/* Theme icon */
.theme-icon {
  position: absolute;
  top: 20px;
  right: 20px;
  font-size: 20px;
  cursor: pointer;
  padding: 8px;
  border-radius: 50%;
  transition: 0.2s;
}

.theme-icon:hover {
  transform: scale(1.1);
}
</style>
