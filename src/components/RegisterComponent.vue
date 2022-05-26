<template>
  <div class="row mt-4">
    <div class="col-6 mx-auto">
      <form @submit.prevent="registerUser">
        <transition name="slide-fade">
          <div v-show="step === 1" class="step">
            <div class="form-group">
              <label for="email">Email address:</label>
              <input v-model="email" type="email" class="form-control" id="email" required>
            </div>

            <div class="form-group">
              <label for="name">Name:</label>
              <input v-model="name" type="text" class="form-control" id="name">
            </div>

            <div class="form-group">
              <label for="surname">Surname:</label>
              <input v-model="surname" type="text" class="form-control" id="surname">
            </div>


            <div class="form-group">
              <label for="password">Password:</label>
              <input v-model="password" type="password" class="form-control" id="password" required>
            </div>

            <div class="form-group">
              <label for="passwordConfirm">Confirm password:</label>
              <input v-model="confirmPassword" type="password" class="form-control" id="passwordConfirm" required>
            </div>

            <button type="submit" class="btn btn-primary mr-2">Sign up</button>
            <button @click="nextStep" type="button" class="btn btn-success">Already have an account</button>
          </div>
        </transition>
      </form>
    </div>


    <div class="col-6 mx-auto">
      <form @submit.prevent="loginUser" novalidate>
        <transition name="slide-fade">
          <div v-show="step === 2" class="step">
            <div class="form-group">
              <label>Email address:</label>
              <input v-model="authUserData.email" type="email" class="form-control" required>
            </div>

            <div class="form-group">
              <label for="password">Password:</label>
              <input v-model="authUserData.password" type="password" class="form-control" required>
            </div>

            <button type="submit" class="btn btn-success mr-3">Log in</button>
            <button @click="registrationStep" type="button" class="btn btn-primary">Sign up</button>
          </div>
        </transition>
      </form>
    </div>


  </div>
</template>

<script>
export default {
  data() {
    return {
      step: 1,
      email: "",
      name: "",
      surname: "",
      password: "",
      confirmPassword: "",
      isAuthorized: false,
      authUserData: {
        email: "",
        password: ""
      }
    }
  },
  methods: {
    nextStep() {
      if (this.step < 2)
        this.step++
    },
    registrationStep() {
      if (this.step > 1)
        this.step--
    },
    registerUser() {
      const user = {
        email: this.email,
        name: this.name,
        surname: this.surname,
        password: this.password
      }
      if (this.password === this.confirmPassword){
        if (this.email=== "" || this.password ===""){
          alert("Please type all required fields!")
        }else{
          if (localStorage.getItem("users")){
            const arr = JSON.parse(localStorage.getItem("users"))
            arr.push(user);
            localStorage.setItem("users",arr)
            localStorage.setItem("users",JSON.stringify(arr))
          }else {
            localStorage.setItem("users",JSON.stringify([user]))
          }
          alert("Registration success, please sign in!")
          this.email = "";
          this.name = "";
          this.surname = "";
          this.password = "";
          this.confirmPassword = "";
          this.step +=1;
        }
      }else{
        alert("Passwords do not match!")
      }
    },
    loginUser() {
      const user = {...this.authUserData}
      let isAuth = this.isAuthorized
      const registered_users = localStorage.getItem("users") ? JSON.parse(localStorage.getItem("users")) : []
      console.log(user)
      if (user.email && user.password){
        registered_users.forEach((item) => {
          if (item.email === user.email && item.password === user.password){
            alert("You're welcome!")
            localStorage.setItem("isAuthorized", true)
            isAuth = true;
            this.$emit("checkA")
          }
        })
        if (!isAuth){
          alert("User doesn't exist")
        }
      }else{
        alert("Please type all fields!")
      }
    }
  }
}
</script>

<style scoped>
.slide-fade-enter-active {
  transition: all 1s ease;
}




.slide-fade-enter{
  transform: translateX(10px);
  opacity: 0;
}
</style>