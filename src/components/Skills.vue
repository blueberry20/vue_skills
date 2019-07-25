<template>
  <div class="hello">
    {{ name }}

    <!-- <button v-on:click="changeName" v-bind:disabled="btnState">Change Name</button> -->
    <div class="holder">
        <!-- prevent to prevent page from reloading, on submit call addSkill method -->
        <form @submit.prevent="addSkill">
            <input type="text" placeholder="Enter a skill" v-model="skill" v-validate="'min:5'" name="skill" >
            
            <input type="checkbox" id="checkbox" v-model="checked">

            <!-- animation enter-active-class is from animate.css library -->
            <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
                <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill')}}</p>
            </transition>
        </form>
        <!-- loop -->
        <ul>
            <li v-for="(data, index) in skills" :key='index'>{{ index }}. {{ data.skill }}</li>
        </ul>

        <!-- display if true -->
        <p v-if="skills.length >1">You have more than one skill</p>
        <p v-else>You have less than one skill</p>

        <!-- add css class if boolean is true -->
        <div v-bind:class="{ 'alert': showAlert}"></div>

        <div v-bind:style="{ backgroundColor: bgColor, width: bgWidth, height: bgHeight}"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data(){
      return {
          checked:false,
          skill: "",
          name: "Coursetro",
          btnState: true,
          skills: [
              {"skill": "Vue.js"},
              {"skill": "React"}
          ],
          showAlert: true,
          bgColor: 'yellow',
          bgWidth: '100%',
          bgHeight: '30px'
      }
  },
  methods: {
      addSkill(){
          this.$validator.validateAll().then((result) => {
              if (result) {
                this.skills.push({skill: this.skill});
                this.skill = '';
              }
              else {
                  console.log("not valid");
              }
          })
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only 
<style src="../skills.css">
</style>-->

<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.2/animate.css";

    .alert {
        background-color: yellow;
    }

    .alert-in-enter-active {
        animation: bounce-in .5s ;
    }

     .alert-in-enter-active {
        animation: bounce-in .5s reverse;
    }

    @keyframes bounce-in {
        0% {
            transform: scale(0);
        }
        50% {
            transform: scale(1.5);
        }
        100% {
            transform: scale(1);
        }
    }
</style>
