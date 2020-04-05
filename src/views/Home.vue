<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <div id="app" class="small-container">
      <h1>Users List Training</h1>
      <users-form @add:user="addUser"/>
      <users-table v-bind:users="users" @delete:user="deleteUser" @edit:usere="editUser"/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import UsersTable from "@/components/Users.vue";
import UsersForm from "@/components/UsersForm.vue";

export default {
  name: "Home",
  components: {
    UsersTable,
    UsersForm
  },
  data() {
    return {
      users: [
        {
          id: 1,
          name: 'Richard Hendricks',
          email: 'richard@piedpiper.com',
        },
        {
          id: 2,
          name: 'Bertram Gilfoyle',
          email: 'gilfoyle@piedpiper.com',
        },
        {
          id: 3,
          name: 'Dinesh Chugtai',
          email: 'dinesh@piedpiper.com',
        },
      ],
    }
  },
  methods: {
    addUser(user){
      const lastId =
      this.users.length > 0
      ? this.users[this.users.length - 1].id
      : 0;

      const id = lastId + 1;
      const newUser = { ...user, id };

      this.users = [...this.users, user]
    },
    deleteUser(id) {
    this.users = this.users.filter(
      user => user.id !== id
    )
  },
  editUser(id, updatedUser) {
  this.users = this.users.map(user =>
    user.id === id ? updatedUser : user
  )
}
  }
};
</script>

<style lang="less" scoped>
button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
  img {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }
</style>
