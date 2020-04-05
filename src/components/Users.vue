/* eslint-disable prettier/prettier */

<template>
  <div id="users-table">
    <p v-if="users.length < 1" class="empty-table">No Users</p>
    <table v-else>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td v-if="editing === user.id">
            <input type="text" v-model="user.name" />
          </td>
          <td v-else>{{ user.name }}</td>

          <td v-if="editing === user.id">
            <input type="text" v-model="user.email" />
          </td>
          <td v-else>{{ user.email }}</td>

          <td v-if="editing === user.id">
            <button @click="editUser(user)">Save</button>
            <button class="muted-button" @click="editing = null">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(user)">Edit</button>
            <button @click="$emit('delete:user', user.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class UsersTable extends Vue {
  @Prop() public users!: [];

  public editing = null;
  public cachedEUser = {};

  editMode(user: any) {
    console.log("test edit mode");
    this.cachedEUser = Object.assign({}, user)

    this.editing = user.id;
  }

  editUser(user: any) {
    if (user.name === "" || user.email === "") return;
    this.$emit("edit:user", user.id, user);
    this.editing = null;
  }

  cancelEdit(user: any) {
    Object.assign(user, this.cachedEUser)
    this.editing = null;
  }
}
</script>

<style scoped lang="less">
button {
  margin: 0 0.5rem 0 0;
}
</style>
