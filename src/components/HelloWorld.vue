<template>
    <!-- <Transition 
                name="submited"
            >
      <div v-if="react.isSubmited" class="container">

          <div  class="contact-us-page form-block-container" >
              <div class="success-message">Thank you! Your submission has been received!</div>
          </div>
      </div>
      <div v-="react.isSubmited" class="container">

          <div  class="contact-us-page form-block-container" >
              <div class="success-message">Thank you! Your submission has been received!</div>
          </div>
      </div>

    </Transition> -->


    <div class="container">
    

      <div v-if="!react.isSubmited">
        <Transition name="slide-fade">
          <div v-show="isShowForm">
            <submit-form class="form"  @submited="react.isSubmited = true"></submit-form>
          </div>
        </Transition>
      </div>

      <div class="header">
            <div class="banner"> </div>
            <div class="welcome-text">

            <Transition name="bounce">
              <div v-if="react.isSubmited" class="">
                  <div class="text-bolded" >Thank you!</div>
                  <div style="margin-top:20px;">You have successfully joined the waitlist!</div>
              </div>
            </Transition>

              <div v-if="!react.isSubmited">
                <div class="text-bolded">Welcome to the Future of Beauty</div>
                <div style="margin-top:40px;">
                  <div>Beauty meets Cutting-Edge Fascia Research.</div>
                  <div style="margin-top:10px;">Learn How to Transform Your Face, Naturally</div>
                </div>

                <div class="submit-btn-container">
                    <button class="button-87" role="button"  @click="handleClick">Join The Waitlist</button>
                </div>
              </div>
            </div>
      </div>

    </div>
</template>

<script setup>
    import SubmitForm from "@/components/SubmitForm";
    import { ref, reactive } from 'vue';

    const react = reactive({ isSubmited: false })


    const isShowForm = ref(false);
    function handleClick() {
        isShowForm.value = !isShowForm.value;
    }


</script>

<style scoped>
.container {
  max-width: 100vw;
  max-height: 100vh;
  width: 100vw;
  height: 100vh;
}
.header {
  height: 85vh;
  color: white;
  position: relative;
  display: grid;
}
.welcome-text {
  font-size: 30px;
  color: white;
  position: absolute;
  top: 70%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  font-weight: 400;
  line-height: 30px;
}

.text-bolded {
  font-weight: 700;
  font-size: 54px;
}

.banner {
  background: url("https://beautyfascia.com/customhtmlfiles/images/banner-bg-img1.jpg")  no-repeat top center;
}

.banner::before {
    content: "";
    position: absolute;
    inset: 0;
    background: black;
    opacity: .4;
}
.form {
  position: absolute;
  background: #dfcfcf;
  backdrop-filter: blur(10px);
  z-index:1;
  min-height: 100vh;
  height: 100vh;
  width: 450px;
}

.submit-btn-container {
  padding-top: 30px;
}

.button-87 {
  margin: auto;
  padding: 15px 30px;
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


.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.slide-fade-enter-active {
  transition: all 0.5s ease-in;
  position:absolute;
  z-index:1;
}

.slide-fade-leave-active {
  transition: all 0.3s ease-in;
  position:absolute;
  z-index:1;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(-400px);
}

.succes-message {
  font-size: 30px;
  color: white;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  font-weight: 400;
  line-height: 30px;
}

.bounce-enter-active {
  animation: bounce-in 0.5s;
}
.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.25);
  }
  100% {
    transform: scale(1);
  }
}

</style>
