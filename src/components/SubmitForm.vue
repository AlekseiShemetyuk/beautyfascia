<template>
   <div class="container">
      <div class="text">
         Join us
      </div>
      <form action="#">
         <div class="form-row">
            <div class="input-data">
               <input ref="firstNameRef" type="text" v-model="dataForm.firstName" required>
               <div class="underline"></div>
               <label for="">First Name</label>
            </div>
         </div>
         <div class="form-row">
            <div class="input-data">
               <input ref="lastNameRef" type="text" v-model="dataForm.lastName" required>
               <div class="underline"></div>
               <label for="">Last Name</label>
            </div>
         </div>
         <div class="form-row">
            <div class="input-data">
               <input ref="emailRef" type="text" v-model="dataForm.email" required>
               <div class="underline"></div>
               <label for="">Email Address</label>
            </div>
         </div>

            <div class="form-row">

                <button class="button-87" v-if="!react.isLoading"  @click="handleSubmit">Submit</button>
                <div v-else class="button-loaded">
                    <div class="loader">
                      
                    </div>
                    <div class="loader-text">
                      Loading...
                    </div>
                  </div>
            </div> 
      </form>
      </div>
</template>

<script setup>
import { useTemplateRef, defineEmits, onMounted, reactive } from 'vue'

const emit = defineEmits(['change']);

const react = reactive({ isLoading: false  })


const firstNameRef = useTemplateRef('firstNameRef');
const lastNameRef = useTemplateRef('lastNameRef')
const emailRef = useTemplateRef('emailRef')

const dataForm = reactive({
    firstName: "",
    lastName: "",
    email: "",
    ip: "",
    country: "",
})

onMounted(() => {
    fetch('https://api.country.is/')
    .then((res) => (res.json()))
    .then((data) => {
        dataForm.ip = data.ip;
        dataForm.country = data.country;
    })

})

async function handleSubmit(event) {
    event.preventDefault();
    event.stopPropagation();

    let isFormValid = [firstNameRef, lastNameRef, emailRef].reduce((result, component) => {
            component.value.reportValidity();
        return result && component.value.value;
    }, true) 
 
    if (isFormValid) {
        react.isLoading = true;
        console.log(isFormValid);

        await createLead(dataForm);
        emit('submited', true);
    }
}
async function createLead(data) {
    try {
        // const URL = 'https://stonehenge.my.site.com/services/apexrest';
        const URL = 'https://beautyfascia-dev-ed.develop.my.site.com/services/apexrest/lead/';

        let response = await fetch(URL, {
            method: 'POST',
            headers: {
            'Content-Type': 'application/json;charset=utf-8',
            'Access-Control-Allow-Origin': '*'
            },
            body: JSON.stringify(data)
        });

        return await response.json(); 
    } catch (err) {
        console.log(err);
    }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Poppins:400,500,600,700&display=swap');
*{
  margin: 0;
  padding: 0;
  outline: none;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}
body{
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 10px;
  font-family: 'Poppins', sans-serif;
  background: linear-gradient(115deg, #FE2C55 10%, #f09819 90%);

}

.container .text{
  text-align: center;
  font-size: 41px;
  font-weight: 600;
  font-family: 'Poppins', sans-serif;
  background: -webkit-linear-gradient(right, #FE2C55, #FE2C55, #f09819, #FE2C55);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
.container form{
  padding: 30px 0 0 0;
}
.container form .form-row{
  display: flex;
  margin: 32px 0;
}
form .form-row .input-data{
  width: 100%;
  height: 40px;
  margin: 0 20px;
  position: relative;
}
form .form-row .textarea{
  height: 70px;
}
.input-data input,
.textarea textarea{
  display: block;
  width: 100%;
  height: 100%;
  border: none;
  font-size: 17px;
  background: none;
  border-bottom: 2px solid rgba(0,0,0, 0.12);
}
.input-data input:focus ~ label, .textarea textarea:focus ~ label,
.input-data input:valid ~ label, .textarea textarea:valid ~ label{
  transform: translateY(-20px);
  font-size: 14px;
  color: #FE2C55;
}
.textarea textarea{
  resize: none;
  padding-top: 10px;
}
.input-data label{
  position: absolute;
  pointer-events: none;
  bottom: 10px;
  font-size: 16px;
  transition: all 0.3s ease;
}
.textarea label{
  width: 100%;
  bottom: 40px;
  background: #fff;
}
.input-data .underline{
  position: absolute;
  bottom: 0;
  height: 2px;
  width: 100%;
}
.input-data .underline:before{
  position: absolute;
  content: "";
  height: 2px;
  width: 100%;
  background: #FE2C55;
  transform: scaleX(0);
  transform-origin: center;
  transition: transform 0.3s ease;
}
.input-data input:focus ~ .underline:before,
.input-data input:valid ~ .underline:before,
.textarea textarea:focus ~ .underline:before,
.textarea textarea:valid ~ .underline:before{
  transform: scale(1);
}
.submit-btn .input-data{
  overflow: hidden;
  height: 45px!important;
  width: 25%!important;
}
.submit-btn .input-data .inner{
  height: 100%;
  width: 300%;
  position: absolute;
  left: -100%;
  background: -webkit-linear-gradient(right, #56d8e4, #9f01ea, #56d8e4, #9f01ea);
  transition: all 0.4s;
}
.submit-btn .input-data:hover .inner{
  left: 0;
}
.submit-btn .input-data input{
  background: none;
  border: none;
  color: #fff;
  font-size: 17px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1px;
  cursor: pointer;
  position: relative;
  z-index: 2;
}
@media (max-width: 700px) {
  .container .text{
    font-size: 30px;
  }
  .container form{
    padding: 10px 0 0 0;
  }
  .container form .form-row{
    display: block;
  }
  form .form-row .input-data{
    margin: 35px 0!important;
  }
  .submit-btn .input-data{
    width: 40%!important;
  }
}




.button-87,.button-loaded {
  margin: auto;
  padding: 12px 50px;
  font-size: 20px;
  text-align: center;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  border-radius: 7px;
  display: block;
  border: 0px;
  font-weight: 700;
  box-shadow: 0px 0px 14px -7px #f09819;
  background-image: linear-gradient(45deg, #FE2C55 0%,  #f09819  51%, #FE2C55  100%);
  cursor: pointer;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.button-87:hover {
  background-position: right center;
  color: #fff;
  text-decoration: none;
}

.button-87:active {
  transform: scale(0.95);
}

.button-loaded {
    padding: 5px 50px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

.loader {
    border: 1px solid white;
    border-radius: 50%;
    border-right-color: transparent;
    border-bottom-color: transparent;
    width: 35px;
    height: 35px;
    animation-name: loading;
    animation-duration: 700ms;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
  }
  
  .loader-text {
    color: lightgrey;
    font-family: 'Lato', sans-serif;
    font-size: 18px;
    animation-name: fading;
    animation-duration: 1500ms;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
  }
  
  
  @keyframes loading{
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }
  
  @keyframes fading {
    0%, 100% {
      opacity: 0.05;
    }
    50% {
      opacity: 0.95;
    }
  }
</style>