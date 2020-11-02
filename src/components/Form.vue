<template>
  <div id="container">
    <button class="button" id="addUser" @click="showModal = true">
      Add User
    </button>
    <transition name="fade" appear>
      <div class="modal-overlay" v-if="showModal" @click="closeForm()"></div>
    </transition>
    <transition name="slide" appear>
      <div class="modal" v-if="showModal">
        <form class="form" id="form" v-on:submit.prevent="addNewUser">
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

        <button class="button" @click="closeForm">
          Close Form
        </button>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "Form",
  props: ["users", "editUser", "action", "showModalProp", "editIndex"],
  data() {
    return {
      showModal: false,
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
      if (newVal === "edit") {
        this.name = this.editUser.name;
        this.email = this.editUser.email;
        this.dob = this.editUser.dob;
        this.showModal = !this.showModal;
      } else {
        this.name = "";
        this.email = "";
        this.dob = "";
      }
    },
    showModalProp(newVal) {
      this.showModal = newVal;
    },
  },

  methods: {
    addNewUser() {
      if (this.name === "") {
        return alert("Enter Name");
      } else if (this.email === "") {
        return alert("Enter Email");
      } else if (this.dob === "") {
        return alert("Enter Date of Birth");
      } else if (this.password === "") {
        return alert("Enter Password");
      } else if (this.password != this.repassword) {
        return alert("Both password should match exaclty");
      } else if (document.getElementById("checkbox").checked == false) {
        return alert("Read and accept the terms & conditions to continue ");
      } else {
        this.$emit("add-new-user", {
          name: this.name,
          email: this.email,
          dob: this.dob,
          password: this.password,
          repassword: this.repassword,
        });
      }
      this.name = "";
      this.email = "";
      this.dob = "";
      this.address = "";
      this.password = "";
      this.repassword = "";
      this.showModal = false;
    },
    closeForm() {
      this.$emit("closeModal", false);
      this.showModal = false;
      this.name = "";
      this.email = "";
      this.dob = "";
      this.address = "";
      this.password = "";
      this.repassword = "";
      document.getElementById("form").reset();
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
.form input[type="submit"]:hover {
  background: #109177;
}
.activeBackground {
  background-color: red;
  color: white;
}
#container {
  position: relative;
  justify-content: center;
  align-items: center;
  width: 100vw;
  min-height: 100vh;
}
.button {
  margin-top: 20px;
  appearance: none;
  outline: none;
  border: none;
  background: none;
  cursor: pointer;
  display: inline-block;
  padding: 15px 25px;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
  border-radius: 8px;
  color: #fff;
  font-size: 18px;
  font-weight: 700;
  box-shadow: 3px 3px rgba(0, 0, 0, 0.4);
  transition: 0.4s ease-out;
}
.button:hover {
  box-shadow: 6px 6px rgba(0, 0, 0, 0.6);
}
.modal-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 98;
  background-color: rgba(0, 0, 0, 0.3);
}
.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 99;
  max-width: 400px;
  background-color: #fff;
  border-radius: 16px;
  padding: 25px;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
.slide-enter-active,
.slide-leave-active {
  transition: transform 0.5s;
}
.slide-enter,
.slide-leave-to {
  transform: translateY(-50%) translateX(100vw);
}
#container #addUser {
  position: fixed;
  top: 50%;
  left: 68%;
}
</style>
