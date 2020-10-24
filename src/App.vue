<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
    <Form
      :users="users"
      @add-new-user="addNewUser"
      :name="name"
      :email="email"
      :dob="dob"
      :password="password"
      :repassword="repassword"
      :editUser="editUser"
      :action="action"
    />
    <Table :users="users" @remove="deleteuser" @edit-item="edit" />
  </div>
</template>

<script>
// import Vue from "vue"
import Form from "./components/Form.vue";
import Table from "./components/Table.vue";
export default {
  name: "App",
  components: {
    Form,
    Table,
  },
  data() {
    return {
      name: "",
      email: "",
      dob: "",
      password: "",
      repassword: "",
      editIndex: -1,
      users: [
        {
          id: 1,
          name: "Kurtis Weissnat",
          email: "km@gmail.com",
          dob: "10/12/1996",
          address: "Rex Trail",
          password: "123456",
          active: false,
        },
        {
          id: 2,
          name: "Nicholas Reichet",
          email: "nr@gmail.com",
          dob: "18/05/1994",
          address: "Bartholomebury",
          password: "12345678",
          active: false,
        },
      ],
      nextUserId: 3,
      editUser: {},
      action: "",
    };
  },
  methods: {
    edit(object) {
      console.log("In edit", object);
      console.log(object);
      // Vue.set(this.user,this.editIndex, this.name, this.email, this.dob);
      this.editUser = object;
      this.action = "edit";
      console.log(this.editUser, ">>>>>>>>>>>>>>>>>>>");
    },
    addNewUser(obj) {
      console.log(obj,'>>>>>>>>>>>');
      if (this.action === "edit") {
        console.log("edituser", this.editUser);
        this.users.forEach((user) => {
          if (user.id === this.editUser.id) {
            console.log(obj.name);
            user.name = obj.name;
            user.email = obj.email;
            user.dob = obj.dob;
          }
          this.action = ''
        });
      } else {
        var { name, email, dob, password, repassword } = obj;
        if (
          name != "" &&
          email != "" &&
          dob != "" &&
          password != "" &&
          repassword === password
        ) {
          this.users.push({
            id: this.nextUserId++,
            name: name,
            email: email,
            dob: dob,
            password: password,
            active: false,
          });
        } else {
          alert("Invalid Input");
        }

        this.name = "";
        this.email = "";
        this.dob = "";
        this.password = "";
        this.repassword = "";
      }
    },
    handleSelect(bool, index) {
      this.users[index].active = bool;
    },
    deleteuser(users, index, bool) {
      this.users[index].active = bool;
      if (bool) {
        if (window.confirm("Do you really want to Delete?")) {
          users.splice(index, 1);
        }
      } else {
        alert("Only selected entries can be deleted");
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
