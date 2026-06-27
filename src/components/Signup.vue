<template>
  <div class="auth-wrapper">
    <form class="card" @submit.prevent="handleSubmit">

      <h2>Create Account</h2>
      <p class="subtitle">Sign up to start using the platform</p>

      <!-- Email -->
      <div class="field">
        <label>Email</label>
        <input v-model="email" type="email" placeholder="you@example.com" />
        <small v-if="errors.email">{{ errors.email }}</small>
      </div>

      <!-- Password -->
      <div class="field">
        <label>Password</label>
        <input v-model="password" type="password" placeholder="••••••••" />
        <small v-if="errors.password">{{ errors.password }}</small>
      </div>

      <!-- Role -->
      <div class="field">
        <label>Role</label>
        <select v-model="role">
          <option disabled value="">Select role</option>
          <option>Developer</option>
          <option>Designer</option>
        </select>
      </div>

      <!-- Submit -->
      <button type="submit">Create Account</button>

    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      errors: {}
    };
  },

  methods: {
    handleSubmit() {
      this.errors = {};

      if (!this.email.includes("@")) {
        this.errors.email = "Invalid email";
      }

      if (this.password.length < 8) {
        this.errors.password = "Minimum 8 characters required";
      }

      if (Object.keys(this.errors).length === 0) {
        alert("Account created successfully!");
      }
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
