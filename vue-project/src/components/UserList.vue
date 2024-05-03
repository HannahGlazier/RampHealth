<template>
  <div id="app">
    <h2 style="text-align: center;">Ramp Health User List</h2>
    <div class="filter-bar">
      <label>Search Users: </label>
      <input
        type="text"
        v-model="filterText"
        placeholder="Filter by name or email"
      />
    </div>
    <div class="user-list">
      <p v-if="filteredUsers.length === 0">No users found</p>
      <ul>
        <li v-for="user in filteredUsers" :key="user.id">
            <button class="delete" @click="deleteUser(user.id)">Delete</button>
            <p class="user">{{ user.firstName }} {{ user.lastName }} </p>
            <p>{{ user.email }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  data: function () {
    // Hard coded list of users to display
    return {
      users: [
        {
          id: 1,
          firstName: "Jereme",
          lastName: "Allen",
          email: "test@test.com",
        },
        {
          id: 2,
          firstName: "Hannah",
          lastName: "Glazier",
          email: "glazierhannah@gmail.com",
        },
        {
          id: 3,
          firstName: "Mia",
          lastName: "Carter",
          email: "mia@test.com",
        },
        {
          id: 4,
          firstName: "Stanley",
          lastName: "Smith",
          email: "stans@aol.com",
        },
        {
          id: 5,
          firstName: "Stella",
          lastName: "Jean",
          email: "testing2@test.com",
        },
        {
          id: 6,
          firstName: "Fred",
          lastName: "Johnson",
          email: "FJ2@gmail.com",
        },
      ],
      filterText: "",
    };
  },
  methods: {
    // Delete User Function (no persistence)
    deleteUser(id) {
      console.log("in deleteUser", id);
      this.users = this.users.filter(user => user.id !== id);
    },
  },
  computed: {
    // Filter Users Function
    filteredUsers: function () {
      return this.users.filter((user) => {
        const searchText = this.filterText.toLowerCase();
        return (
          user.firstName.toLowerCase().includes(searchText) ||
          user.lastName.toLowerCase().includes(searchText) ||
          user.email.toLowerCase().includes(searchText)
        );
      });
    },
  },
};
</script>
