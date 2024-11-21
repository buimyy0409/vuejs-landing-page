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
const showErrorModal = ref(false);
// Function to handle signup
function signUp() {
  if (!username.value || !password.value) {
    message.value = "Username or password are required!";
    showErrorModal.value = true;
    return;
  }

  const users = JSON.parse(localStorage.getItem("users")) || [];
  if (users.some(user => user.username === username.value)) {
    message.value = "Username already exists (╯︿╰)";
    showErrorModal.value = true;
    return;
  }

  users.push({ username: username.value, password: password.value });
  localStorage.setItem("users", JSON.stringify(users));
  message.value = "Register successful! You can now log in.";
  showErrorModal.value = true;
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
    message.value = "Sign in successfully! o(*^▽^*)o";
    showErrorModal.value = true;
    showLoginModal.value = false; // Close login modal
    clearFields();
  } else {
    
    message.value = "Invalid username or password 🥺";
    showErrorModal.value = true;
  }
}

// Function to handle logout
function logOut() {
  isLoggedIn.value = false;
  currentUser.value = "";
  
  message.value = "You have logged out ヾ(￣▽￣) Bye~";
  showErrorModal.value = true;
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
            <a href="#" class="ml-3 text-danger" @click.prevent="logOut" style="margin-left: 20px;">Log out</a>
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
        <h2>Sign in</h2>
        <div style="margin-top: 10px;">
          <input v-model="username" type="text" placeholder="Username" />
        </div>
        <div style="margin-top: 10px;">
          <input v-model="password" type="password" placeholder="Password" />
        </div>
        <button @click="logIn">Sign in</button>
        <buttonclose @click="showLoginModal = false">Close</buttonclose>
      </div>
    </div>

    <!-- Signup Modal -->
    <div v-if="showSignupModal" class="modal">
      <div class="modal-content">
        <h2>Sign Up</h2>
        <input v-model="username" type="text" placeholder="Username" />
        <input v-model="password" type="password" placeholder="Password" />
        <button @click="signUp">Register</button>
        <buttonclose @click="showSignupModal = false">Close</buttonclose>
      </div>
    </div>

    <div v-if="showErrorModal" class="modal">
    <div class="modal-content" style="line-height: 1.5;">
      <h3 style="margin-bottom: 15px;">{{ message }}</h3>
      <buttonclose @click="showErrorModal = false">Close</buttonclose>
    </div>
    </div>

    <!-- Message 
    <p>{{ message }}</p> -->
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
  margin-top: 15px;
  padding: 5px;
  padding-left: 10px;
  padding-right: 10px;
  cursor: pointer;
  border: 1.8px solid #005f69; 
  background-color: #fff;
  border-radius: 8px;
}

button:hover {
  opacity: 0.8;
  background-color: #005f69; 
  color: #fff; 
  border-color: #005f69 
}

buttonclose {
  margin: 10px;
  margin-top: 15px;
  margin-bottom: 15px;
  padding: 5px;
  padding-left: 10px;
  padding-right: 10px;
  padding-top: 6px;
  padding-bottom: 7px;
  cursor: pointer;
  border: 1.8px solid #005f69; 
  background-color: #fff;
  color: black;
  border-radius: 8px;
}

buttonclose:hover {
  opacity: 0.8;
  background-color: #f26f33;
  color: #fff; 
  border-color: #f26f33; 
}


</style>
