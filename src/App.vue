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
      :showModalProp="showModal"
      :editUser="editUser"
      :action="action"
      @closeModal="closeModal"
      :edit-index="editIndex"
    >
    </Form>

    <Table
      @sort-table="sortTable"
      :users="users"
      @remove="deleteuser"
      @edit-item="edit"
      :currentPage.sync="currentPage"
      :pageSize="5"
      @totalPagesChanged="totalPages = $event"
    />
  </div>
</template>

<script>
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
      showModal: false,
      editIndex: -1,
      currentPage: 1,
      totalPages: 0,
      users: [
        {
          id: 1,
          name: "Kurtis Weissnat",
          email: "km@gmail.com",
          dob: "1996-05-28",
          address: "Rex Trail",
          password: "123456",
          active: false,
        },
        {
          id: 2,
          name: "Nicholas Reichet",
          email: "nr@gmail.com",
          dob: "1994-05-14",
          address: "Bartholomebury",
          password: "12345678",
          active: false,
        },
        {
          id: 3,
          name: "Raman Goyal",
          email: "rg@gmail.com",
          dob: "1997-05-14",
          address: "Bartholomebury",
          password: "12345678",
          active: false,
        },
        {
          id: 4,
          name: "Sahil",
          email: "sg@gmail.com",
          dob: "1995-05-14",
          address: "Bartholomebury",
          password: "12345678",
          active: false,
        },
        {
          id: 5,
          name: "Paru",
          email: "p@gmail.com",
          dob: "1998-05-14",
          address: "Bartholomebury",
          password: "12345678",
          active: false,
        },
        {
          id: 6,
          name: "Honey",
          email: "ha@gmail.com",
          dob: "1999-05-14",
          address: "Bartholomebury",
          password: "12345678",
          active: false,
        },
        {
          id: 7,
          name: "Manu",
          email: "mg@gmail.com",
          dob: "1991-05-14",
          address: "Bartholomebury",
          password: "12345678",
          active: false,
        },
        {
          id: 8,
          name: "Manu1",
          email: "mg@gmail.com",
          dob: "1991-05-14",
          address: "Bartholomebury",
          password: "12345678",
          active: false,
        },
      ],
      nextUserId: 9,
      editUser: {},
      action: "",
    };
  },
  methods: {
    edit(obj) {
      this.showModal = true;
      this.editUser = obj;
      this.action = "edit";
      this.name = this.editUser.name;
      this.email = this.editUser.email;
      this.dob = this.editUser.dob;
    },
    addNewUser(obj) {
      if (this.action === "edit") {
        this.users.forEach((user) => {
          if (user.id === this.editUser.id) {
            user.name = obj.name;
            user.email = obj.email;
            user.dob = obj.dob;
          }
          this.action = "";
        });
      } else {
        const { name, email, dob, password, repassword } = obj;
        if (
          name != "" &&
          email != "" &&
          dob != "" &&
          password != "" &&
          repassword === password &&
          this.$refs["checkbox"].checked
          // document.getElementById("checkbox").checked
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
    closeModal(val) {
      this.showModal = val;
      this.action = "";
    },
    deleteuser(users, user) {
      let userToBeDeleted = users.indexOf(user);
      if (window.confirm("Do you really want to Delete?")) {
        users.splice(userToBeDeleted , 1);
      }
    },
    sortTable(users) {
      users.sort(function(a, b) {
        if (new Date(a.dob) < new Date(b.dob)) {
          return -1;
        }
        if (new Date(a.dob) > new Date(b.dob)) {
          return 1;
        }
        return 0;
      });
    },
  },
};
</script>

<style>
body {
  display: block;
  margin: 0px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
