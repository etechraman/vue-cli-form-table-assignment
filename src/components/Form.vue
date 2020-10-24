<template>
  <div>
    <form class="form" v-on:submit.prevent="addNewUser">
      <fieldset>
        <legend>Candidate Info</legend>
        <input
          type="text"
          name="field1"
          placeholder="Enter Your Full Name *"
          v-model="name"
        />
        <input
          type="email"
          name="field2"
          placeholder="Enter Your Email Address *"
          v-model="email"
        />
        <input type="date" name="field3" required v-model="dob" />
        <input
          type="password"
          name="field4"
          placeholder="Enter a password *"
          v-model="password"
        />
        <input
          type="password"
          name="field5"
          placeholder="Re-Enter the password *"
          v-model="repassword"
        />
        <input type="checkbox" id="checkbox" name="field6" />
        <label for="checkbox"
          >Tick the checkbox if you agree to terms conditions *</label
        >
      </fieldset>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
export default {
  name: "Form",
  props: ["users", "editUser", 'action'],
  data() {
    return {
      name: "",
      email: "",
      dob: "",
      address: "",
      password: "",
      repassword: "",
    };
  },
  watch: {
    action(newVal) {
      if(newVal==="edit"){
        this.name=this.editUser.name;
        this.email=this.editUser.email;
        this.dob=this.editUser.dob;
      }
    },
  },

  methods: {
    addNewUser() {
      if (this.editIndex !== -1) {
          this.$emit("edit-item", {
            name: this.name,
            email: this.email,
            dob: this.dob,
            editIndex: this.editIndex,
          });
        
      } else console.log("adding new user");
      if (this.name === "") {
        alert("Enter Name");
      } else if (this.email === "") {
        alert("Enter Email");
      } else if (this.dob === "") {
        alert("Enter Date of Birth");
      } else if (this.password === "") {
        alert("Enter Password");
      } else if (this.password != this.repassword) {
        alert("Both password should match exaclty");
      } else {
        this.$emit("add-new-user", {
          name: this.name,
          email: this.email,
          dob: this.dob,
          password: this.password,
          repassword: this.repassword,
        });
      }
      console.log(
        this.name,
        this.email,
        this.dob,
        this.address,
        this.password,
        this.repassword
      );
      this.name = "";
      this.email = "";
      this.dob = "";
      this.address = "";
      this.password = "";
      this.repassword = "";
    },
  },
};
</script>
<style>
.form {
  max-width: 500px;
  padding: 10px 20px;
  background: #f4f7f8;
  margin: 10px auto;
  padding: 20px;
  background: #f4f7f8;
  border-radius: 8px;
  font-family: Georgia, "Times New Roman", Times, serif;
}
.form fieldset {
  border: none;
}
.form legend {
  font-size: 1.4em;
  margin-bottom: 10px;
}
.form label {
  display: block;
  margin-bottom: 8px;
}
.form input {
  font-family: Georgia, "Times New Roman", Times, serif;
  background: rgba(255, 255, 255, 0.1);
  border: none;
  border-radius: 4px;
  font-size: 15px;
  margin: 0;
  outline: 0;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  background-color: #e8eeef;
  color: #8a97a0;
  -webkit-box-shadow: 0 1px 0 rgba(0, 0, 0, 0.03) inset;
  box-shadow: 0 1px 0 rgba(0, 0, 0, 0.03) inset;
  margin-bottom: 30px;
}
.form input:focus {
  background: #d2d9dd;
}
.form input[type="submit"],
.form input[type="button"] {
  position: relative;
  display: block;
  padding: 19px 39px 18px 39px;
  color: #fff;
  margin: 0 auto;
  background: #1abc9c;
  font-size: 18px;
  text-align: center;
  font-style: normal;
  width: 100%;
  border: 1px solid #16a085;
  border-width: 1px 1px 3px;
  margin-bottom: 10px;
}
.form input[type="submit"]:hover,
.form input[type="button"]:hover {
  background: #109177;
}
#table {
  width: 918.5px;
  margin-left: auto;
  margin-right: auto;
  border-collapse: collapse;
}

tr {
  background-color: #ffe839;
}

th {
  text-align: left;
  padding: 0em 1em;
  border: 1px solid black;
}

.activeBackground {
  background-color: red;
  color: white;
}
</style>
