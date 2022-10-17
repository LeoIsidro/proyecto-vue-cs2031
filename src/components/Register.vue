<template>
    <div class="Register content-center">
      <label for="newUsername">Username: </label>
      <input v-bind:value="newUsername" v-on:input="onUsernameInput" name="newUsername" id="newUsername" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500  w-20">
      <br><br>
      <label for="newEmail" >Email:</label>
      <input v-bind:value="newEmail" v-on:input="onEmailInput"  name="newEmail" id="newEmail" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500  w-20">
      <br><br>
      <label for="newPassword" type="password">Password: </label>
      <input v-bind:value="newPassword" v-on:input="onPasswordInput"  name="newPassword" id="newPassword" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500  w-20">
      <br><br>
      <button v-on:click="onRegister" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Register!</button>
      <br><br>
      <div v-if="success && RegisterAttempt" id="success">Success!</div>
      <div v-if="!success && RegisterAttempt" id="fail">Incorrect username or password</div>
    </div>
  </template>

  
 <script>
 export default {
    name: 'RegisterComponent',
    props: {
    },
  data () {
      return {
          newUsername: "",
          newPassword: "",
          newEmail:"",
          success: false,
          RegisterAttempt: false
      }
  },
  methods: {
      onUsernameInput(e) {
          this.RegisterAttempt = false;
          this.newUsername = e.target.value;
      },
      onPasswordInput(e) {
          this.RegisterAttempt = false;
          this.newPassword = e.target.value;
      },
      onEmailInput(e) {
          this.RegisterAttempt = false;
          this.newEmail = e.target.value;
      },
      onRegister() {
          const url = "http://localhost:5000/login/register";

          const body = {
              "newUsername": this.newUsername,
              "newPassword": this.newPassword,
              "newEmail": this.newEmail,
          };

          fetch(url, {
              method: "POST",
              body: JSON.stringify(body),
              headers: {
                  "Content-Type": "application/json"
              }
          }).then((resp) => resp.json())
          .then((data) => {
              this.RegisterAttempt = true;
              //operador ternario (ternary operator)
              // this.success = data.success ? true : false;

              this.success = data.success;
          });
      }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #success {
      color: blue;
  }

  #fail {
      color: red;
  }
</style>
