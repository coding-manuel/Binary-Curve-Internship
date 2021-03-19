<template>
<form id="form-container" v-on:submit.prevent>
  <div class="name-container">
    <label for="name">Hi, my name is </label>
    <input type="text" id="name" class="text-inp" v-on:keyup.enter="emailShow" v-model="name">
  </div>
  <div class="email-container">
    <label for="email">My email is </label>
    <input type="text" id="email" class="text-inp" v-on:keyup.enter="ageShow" v-model="email">
  </div>
  <div class="age-container">
    <label for="age">My age is </label>
    <input type="text" id="age" class="text-inp" v-on:keyup.enter="buttonShow" v-model="age">
  </div>
</form>
<button v-on:click="onsubmit" id="submit">Submit</button>

<div class="display">
  <h1>{{ name }} you are {{ age }} years old and we will send you all the information on {{ email }} </h1>
</div>
</template>

<script>
import { watch, ref } from 'vue';

export default {
  setup(){

    var hasNumber = /\d/;
    var validRegex = /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;

    const name = ref('');
    const email = ref('');
    const age = ref(null);

    function emailShow(){
      if(name.value.length > 0 && !(hasNumber.test(name.value))){
        document.querySelector(".email-container").style.display = "block";
        document.querySelector("#email").focus();
      }
    }

    function ageShow(){
      if(email.value.match(validRegex) || email.value.length == 0){
        document.querySelector(".age-container").style.display = "block";
        document.querySelector("#age").focus();
      }
    }

    function buttonShow(){
      if(age.value > 0 && age.value < 117)
        document.querySelector("#submit").style.display = "block";
    }

    function onsubmit(){
      document.querySelector("#form-container").style.display = "none";
      document.querySelector("#submit").style.display = "none";
      document.querySelector(".display").style.display = "block";
    }

    watch([name, email, age], (currentValue, oldValue) => {

      if(name.value.length == 0 || hasNumber.test(name.value)){
        document.getElementById("name").style.color = "#DF2935";
        document.getElementById("name").style.borderColor = "#DF2935";
      }
      else{
        document.getElementById("name").style.color = "#79db63";
        document.getElementById("name").style.borderColor = "#79db63";
      }

      if(email.value.match(validRegex) || email.value.length == 0){
        document.getElementById("email").style.color = "#79db63";
        document.getElementById("email").style.borderColor = "#79db63";
      }
      else{
        document.getElementById("email").style.color = "#DF2935";
        document.getElementById("email").style.borderColor = "#DF2935";
      }

      if(age.value == null || age.value > 0 && age.value < 117){
        document.getElementById("age").style.color = "#79db63";
        document.getElementById("age").style.borderColor = "#79db63";
      }
      else{
        document.getElementById("age").style.color = "#DF2935";
        document.getElementById("age").style.borderColor = "#DF2935";
      }

      console.log(currentValue);
      console.log(oldValue);
    });

    return{
      emailShow,
      ageShow,
      onsubmit,
      buttonShow,
      name,
      email,
      age
    }
  }
}
</script>

<style>

@import url(https://fonts.googleapis.com/css2?family=Raleway:wght@600;800&display=swap);

body{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  size: 1vw;
  background: #222222;
}

#app {
  font-family: 'Raleway', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #EAEAEA;
  margin: 4rem;
}

form{
  width: 80vw;
  margin: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  font-size: clamp(1rem, 2vw, 5rem);
  font-weight: 800;
}

form > div{
  margin: .5rem;
}

.text-inp{
  font-size: clamp(1rem, 2vw, 5rem);
  font-weight: 600;
  color: #EAEAEA;
  outline: none;
  border: none;
  border-bottom: solid #EAEAEA;
  background: transparent;
}

button{
  font-size: clamp(1rem, 2vw, 5rem);
  font-weight: 600;
  color: #222222;
  width: 30vw;
  margin: 1rem auto;
  padding: 1rem 1rem;
  background: rgb(175, 175, 175);
  border: 2px white solid;
  border-radius: 5px;
  background: #EAEAEA;
  cursor: pointer;
  transition: .1s ease-in;
}

button:hover{
  color: #EAEAEA;
  background: #222222;
}

.display{
  font-size: clamp(1rem, 1vw, 5rem);
}

.email-container, .age-container, #submit, .display{
  display: none;
}
</style>
