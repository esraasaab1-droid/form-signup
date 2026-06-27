<template>
  <form @submit.prevent="handleSUbmit">

    <!-- Email -->
    <label>
      <i class="fa-solid fa-envelope"></i>
      Email:
    </label>
    <input v-model="email" type="email" required />

    <!-- Password -->
    <label>
      <i class="fa-solid fa-lock"></i>
      Password:
    </label>
    <input v-model="password" type="password" required />

    <div v-if="PasswrdError" class="error">
      <i class="fa-solid fa-triangle-exclamation"></i>
      {{ PasswrdError }}
    </div>

    <!-- Role -->
    <label>
      <i class="fa-solid fa-user-tie"></i>
      Role:
    </label>
    <select v-model="role" required>
      <option disabled value="">Select role</option>
      <option>Web Developer</option>
      <option>Web Designer</option>
    </select>

    <!-- Terms -->
    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label>
        <i class="fa-solid fa-circle-check"></i>
        I agree to the terms
      </label>
    </div>

    <!-- Skills -->
    <label>
      <i class="fa-solid fa-code"></i>
      Skills:
    </label>

    <div class="skill-input">
      <input
        v-model="tempSkill"
        type="text"
        placeholder="Add skill"
      />

      <button type="button" @click="addskill">
        <i class="fa-solid fa-plus"></i>
        Add
      </button>
    </div>

    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="removeskill(skill)">
        <i class="fa-solid fa-gem"></i>
        {{ skill }}
      </span>
    </div>

    <!-- Submit -->
    <div class="submit">
      <button type="submit">
        <i class="fa-solid fa-user-plus"></i>
        Create Account
      </button>
    </div>

  </form>
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
      terms: false,
      skills: [],
      tempSkill: "",
      PasswrdError: ""
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
        this.PasswrdError =
          "Password must be 8+ chars, uppercase, lowercase, number, and symbol";
        return;
      }

      alert("Account created successfully!");

      console.log({
        email: this.email,
        password: this.password,
        role: this.role,
        terms: this.terms,
        skills: this.skills
      });
    }
  }
};
</script>
<style>
.skill-input {
  display: flex;
  gap: 10px;
  margin-bottom: 10px;
}

.skill-input input {
  flex: 1;
}

.skill-input button {
  background: #4f46e5;
  color: white;
  border: none;
  padding: 10px 14px;
  border-radius: 8px;
  cursor: pointer;
  transition: 0.2s;
  display: flex;
  align-items: center;
  gap: 6px;
}

.skill-input button:hover {
  background: #4338ca;
}

.pill {
  display: inline-block;
  margin: 6px;
  padding: 6px 10px;
  background: #eee;
  border-radius: 20px;
  cursor: pointer;
}</style>
