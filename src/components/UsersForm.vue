/* eslint-disable prettier/prettier */
<template>
  <div id="user-form">
    <form @submit.prevent="handleSubmit">
      <label>User name</label>
      <input
        type="text"
        ref="first"
        v-model="user.name"
        :class="{ 'has-error': submitting && invalidName }"
        @focus="clearStatus"
        @keyup="clearStatus"
      />
      <label>User Email</label>
      <input
        type="text"
        v-model="user.email"
        :class="{ 'has-error': submitting && invalidEmail }"
        @focus="clearStatus"
      />
      <p v-if="error && submitting" class="error-message">❗Please fill out all required fields</p>
      <p v-if="success" class="success-message">✅ Employee successfully added</p>
      <button>Add User</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "users-form",
  data() {
    return {
      submitting: false,
      error: false,
      success: false,
      user: {
        name: "",
        email: ""
      }
    };
  },
  methods: {
    handleSubmit() {
      this.submitting = true;
      this.clearStatus();

      if (this.invalidName || this.invalidEmail) {
        this.error = true;
        return;
      }

      this.$emit("add:user", this.user);
      this.$refs.first.focus()
      this.user = {
        name: "",
        emai: ""
      };
      (this.error = false), (this.success = true), (this.submitting = false);
    },

    clearStatus() {
      this.success = false;
      this.error = false;
    }
  },
  computed: {
    invalidName() {
      return this.user.name === "";
    },
    invalidEmail() {
      return this.user.name === "";
    }
  }
};
</script>

<style scoped lang="less">
form {
  margin-bottom: 2rem;
}
[class*="-message"] {
  font-weight: 500;
}

.error-message {
  color: #d33c40;
}

.success-message {
  color: #32a95d;
}
</style>
