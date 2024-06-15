<template>
  <nav class="navbar">
    <div class="navbar-brand">
      <router-link to="/" class="navbar-item">WEATHER</router-link>
    </div>
    <div class="task-links">
      <div class="dropdown" @click="toggleDropdown">
        <div class="navbar-item">IKHSAN ANSARI ▼</div>
        <div class="dropdown-menu" :class="{ 'is-active': isDropdownActive }">
          <a href="https://ikhsanansari-tugas1.vercel.app/" class="navbar-item" target="_blank">TUGAS 1</a>
          <a href="https://tugas2-pbk-223510216-4g.web.app/" class="navbar-item" target="_blank">TUGAS 2</a>
          <a href="https://ikhsan-ansari-223510216-tugas3.vercel.app/" class="navbar-item" target="_blank">TUGAS 3</a>
          <a href="https://ikhsanansari-pbk-tugas4.vercel.app/" class="navbar-item" target="_blank">TUGAS 4</a>
          <a href="https://ikhsan-pbk-t5.vercel.app/" class="navbar-item" target="_blank">TUGAS 5</a>
          <a href="https://ikhsan-ansari-223510216-tugas-6.vercel.app/" class="navbar-item" target="_blank">TUGAS 6</a>
          <a href="https://ikhsanansari-223510216-tugas7.vercel.app/" class="navbar-item" target="_blank">TUGAS 7</a>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
  data() {
    return {
      isDropdownActive: false
    };
  },
  methods: {
    toggleDropdown() {
      this.isDropdownActive = !this.isDropdownActive;
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

.navbar {
 
  color: rgb(3, 8, 11);
  padding: 10px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-family: 'Poppins', sans-serif;
}

.navbar-brand {
  display: flex;
  align-items: center;
}

.navbar-item {
  color: rgb(175, 84, 19);
  text-decoration: none;
  margin: 0 10px;
  padding: 10px;
  border-radius: 5px;
  transition: background-color 0.3s, color 0.3s;
  font-size: 18px;
}

.navbar-item:hover {
  background-color: #f7dda8;
}

.task-links {
  display: flex;
  align-items: center;
}

.dropdown {
  position: relative;
  cursor: pointer;
}

.dropdown-menu {
  display: none;
  position: absolute;
  top: calc(100% + 10px);
  left: 50%;
  transform: translateX(-50%);
  background-color: #f4ddd6;
  border-radius: 10px;
  padding: 10px 0;
  box-shadow: 0 4px 20px rgba(16, 16, 16, 0.1);
  z-index: 1000;
  width: 200px;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
}

.dropdown-menu.is-active {
  display: block;
  opacity: 1;
  pointer-events: auto;
}

.dropdown-menu .navbar-item {
  display: block;
  width: 100%;
  padding: 10px 20px;
  font-size: 16px;
}

.dropdown-menu .navbar-item:hover {
  background-color: #abbed1;
}

.navbar-item.active {
  background-color: #abbed1;
}
</style>
