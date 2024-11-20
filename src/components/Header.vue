<script setup>
import { ref } from "vue";
import { themeColor, siteName } from "../data/items";

// States for user authentication
const username = ref("");
const password = ref("");
const message = ref("");
const isLoggedIn = ref(false);
const currentUser = ref("");

// Modal visibility states
const showLoginModal = ref(false);
const showSignupModal = ref(false);

// Function to handle signup
function signUp() {
  if (!username.value || !password.value) {
    message.value = "Username and password are required.";
    return;
  }

  const users = JSON.parse(localStorage.getItem("users")) || [];
  if (users.some(user => user.username === username.value)) {
    message.value = "Username already exists.";
    return;
  }

  users.push({ username: username.value, password: password.value });
  localStorage.setItem("users", JSON.stringify(users));
  message.value = "Signup successful! You can now log in.";
  showSignupModal.value = false; // Close signup modal
  clearFields();
}

// Function to handle login
function logIn() {
  const users = JSON.parse(localStorage.getItem("users")) || [];
  const user = users.find(
    user =>
      user.username === username.value && user.password === password.value
  );

  if (user) {
    isLoggedIn.value = true;
    currentUser.value = username.value;
    message.value = `Welcome, ${username.value}!`;
    showLoginModal.value = false; // Close login modal
    clearFields();
  } else {
    message.value = "Invalid username or password.";
  }
}

// Function to handle logout
function logOut() {
  isLoggedIn.value = false;
  currentUser.value = "";
  message.value = "You have logged out.";
}

// Clear input fields
function clearFields() {
  username.value = "";
  password.value = "";
}
</script>

<template>
  <nav class="site-nav dark js-site-navbar mb-5 site-navbar-target">
    <div class="container">
      <div class="site-navigation">
        <a href="" class="logo m-0 float-left">
          {{ siteName }}<span class="text-primary">.</span>
        </a>
        <ul class="js-clone-nav d-none d-lg-inline-block site-menu float-left">
          <li class="active"><a href="#home-section" class="nav-link">Home</a></li>
          <li class="has-children">
            <a href="#" class="nav-link">Dropdown</a>
            <ul class="dropdown">
              <li>
                <a href="#testimonials-section" class="nav-link">Testimonials</a>
              </li>
              <li><a href="#" class="nav-link">Menu Two</a></li>
              <li><a href="#" class="nav-link">Menu Three</a></li>
            </ul>
          </li>
          <li><a href="#features-section" class="nav-link">Features</a></li>
          <li><a href="#pricing-section" class="nav-link">Pricing</a></li>
          <li><a href="#about-section" class="nav-link">About</a></li>
          <li><a href="#contact-section" class="nav-link">Contact</a></li>
        </ul>
        <ul class="js-clone-nav d-none mt-1 d-lg-inline-block site-menu float-right">
          <li v-if="!isLoggedIn" class="cta-button-outline" style="margin-right: 5px;">
            <a href="#" @click.prevent="showLoginModal = true">Sign in</a>
          </li>
          <li v-if="!isLoggedIn" class="cta-primary">
            <a href="#" :style="[{ backgroundColor: themeColor }]" @click.prevent="showSignupModal = true">
              Register
            </a>
          </li>
          <li v-if="isLoggedIn" class="cta-primary">
            <span>Welcome, {{ currentUser }}!</span>
            <a href="#" class="ml-3 text-danger" @click.prevent="logOut">Log out</a>
          </li>
        </ul>
        <a
          href="#"
          class="burger ml-auto float-right site-menu-toggle js-menu-toggle d-inline-block dark d-lg-none"
          data-toggle="collapse"
          data-target="#main-navbar"
        >
          <span></span>
        </a>
      </div>
    </div>

    <!-- Login Modal -->
    <div v-if="showLoginModal" class="modal">
      <div class="modal-content">
        <h2>Login</h2>
        <input v-model="username" type="text" placeholder="Username" />
        <input v-model="password" type="password" placeholder="Password" />
        <button @click="logIn">Login</button>
        <button @click="showLoginModal = false">Close</button>
      </div>
    </div>

    <!-- Signup Modal -->
    <div v-if="showSignupModal" class="modal">
      <div class="modal-content">
        <h2>Sign Up</h2>
        <input v-model="username" type="text" placeholder="Username" />
        <input v-model="password" type="password" placeholder="Password" />
        <button @click="signUp">Sign Up</button>
        <button @click="showSignupModal = false">Close</button>
      </div>
    </div>

    <!-- Message -->
    <p>{{ message }}</p>
  </nav>
</template>

<style>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  width: 300px;
  text-align: center;
}

button {
  margin: 10px;
  padding: 10px;
  cursor: pointer;
}

button:hover {
  opacity: 0.8;
}
</style>
