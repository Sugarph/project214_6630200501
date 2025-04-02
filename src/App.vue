<template>
  <div id="app">
    <header class="main-header">
      <div class="logo">
        <router-link to="/" custom v-slot="{ navigate }">
          <span @click="navigate" role="link" class="logo-link">
            <img src="@/assets/mySignature.png" alt="Logo" />
          </span>
        </router-link>
      </div>
      <nav class="app-main-menu">
        <ul>
          <li>
            <router-link to="/profile" custom v-slot="{ navigate }">
              <span @click="navigate" role="link" class="menu-link">Profile</span>
            </router-link>
          </li>
          <li>
            <router-link to="/about" custom v-slot="{ navigate }">
              <span @click="navigate" role="link" class="menu-link">About</span>
            </router-link>
          </li>
        </ul>
      </nav>
    </header>

    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body {
  overflow-x: hidden;
  scrollbar-width: none;
}

.router-link-active,
.router-link-exact-active {
  color: inherit;
}
</style>

<style scoped>
.main-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 2rem;
  z-index: 1000;
}

.logo {
  flex-shrink: 0;
}

.logo-link {
  display: inline-block;
  cursor: pointer;
}

.logo img {
  height: 120px;
  width: auto;
  transition: transform 0.3s ease;
}

.logo-link:hover img {
  transform: scale(1.05) rotate(2deg);
}

.app-main-menu {
  margin-left: auto;
}

.app-main-menu ul {
  display: flex;
  list-style: none;
  gap: 2.5rem;
  margin: 0;
  padding: 0;
  align-items: center;
}

.app-main-menu .menu-link {
  text-decoration: none;
  font-family: "Eurostile", sans-serif;
  font-weight: 500;
  font-size: 1.5rem;
  position: relative;
  transition: transform 0.3s ease;
  display: inline-block; 
  cursor: pointer;
}

.app-main-menu .menu-link::after {
  content: "";
  position: absolute;
  width: 0;
  height: 2px;
  bottom: -5px;
  left: 0;
  background: currentColor; 
  transition: width 0.3s ease;
}

.app-main-menu .menu-link:hover {
  transform: translateY(-3px);
}

.app-main-menu .menu-link:hover::after {
  width: 100%;
}
</style>