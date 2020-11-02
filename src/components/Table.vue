<template>
  <div>
    <table id="table">
      <thead>
        <tr>
          <th>Full Name</th>
          <th>Email Address</th>
          <th v-on:click="$emit('sort-table', users)">Date of Birth</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(user, index) in getrows()"
          v-bind:key="index"
          :class="{ activeBackground: user.active }"
        >
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.dob }}</td>
          <td>
            <button v-on:click="$emit('remove', users, user)">
              Remove
            </button>
            <button v-on:click.prevent="$emit('edit-item', user)">
              Edit
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <div class="pagination">
      <a id="previousArrow" v-on:click="previousPage()" v-if="activePage > 1"
        >&laquo;</a
      >
      <a
        v-on:click="checkPage(user)"
        v-for="user in totalPages()"
        v-bind:key="user.id"
        >{{ user }}</a
      >
      <a id="nextArrow" v-on:click="nextPage()" v-if="activePage < totalPages()"
        >&raquo;</a
      >
    </div>
  </div>
</template>
<script>
export default {
  name: "Table",
  props: ["users"],
  data() {
    return {
      activePage: 1,
      numberOfData: 5,
    };
  },
  methods: {
    totalPages() {
      return Math.ceil(this.users.length / 5);
    },
    checkPage(id) {
      if (id === 2) {
        let pageNumber = document.getElementsByTagName("a")[id - 1].innerText;
        this.activePage = pageNumber;
      } else {
        let pageNumber = document.getElementsByTagName("a")[id].innerText;
        this.activePage = pageNumber;
      }
    },
    getrows() {
      if (this.users.length) {
        let start = (this.activePage - 1) * this.numberOfData;
        let end = start + this.numberOfData;
        let displayData = this.users.slice(start, end);
        if (!displayData.length) {
          this.activePage = this.activePage - 1;
        } else {
          return displayData;
        }
      }
    },
    nextPage() {
      if (this.activePage < this.totalPages()) {
        this.activePage = this.activePage + 1;
        return this.activePage;
      }
    },
    previousPage() {
      if (this.activePage > 1) {
        this.activePage = this.activePage - 1;
        return this.activePage;
      }
    },
    nextArrow() {
      if (this.activePage >= this.totalPages) {
        return false;
      } else {
        return true;
      }
    },
  },
};
</script>
<style>
#table {
  width: 918.5px;
  position: fixed;
  top: 35%;
  left: 0;
  bottom: 0;
  right: 0;
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

.pagination {
  display: inline-block;
  position: fixed;
  top: 49%;
  left: 46%;
}

.pagination a {
  color: black;
  float: left;
  padding: 8px 16px;
  text-decoration: none;
}
</style>
