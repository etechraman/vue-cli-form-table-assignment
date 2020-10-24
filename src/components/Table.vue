<template>
  <div>
    <table id="table">
      <thead>
        <tr>
          <th>Full Name</th>
          <th>Email Address</th>
          <th>Date of Birth</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(user, index) in users"
          v-bind:key="user.id"
          :class="{ activeBackground: user.active }"
          v-on:select="handleSelect($event, index)"
        >
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.dob }}</td>
          <td>
            <button v-on:click="$emit('remove', users, index, $event)">
              Remove
            </button>
            <button v-on:click.prevent="$emit('edit-item', user)"> 
              Edit
            </button>
            <!-- <input v-model='active' @change="$emit('select',active)" type ="checkbox"> -->
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  name: "Table",
  props: ["users"],
};
</script>
<style></style>
