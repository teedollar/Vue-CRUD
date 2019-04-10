<template>
  <div class="skills">

    <form @submit.prevent="addSkill">
      <input type="" placeholder="Enter a skill you possess" v-model="skill" v-validate="'min:6'" name="skill">
      <transition enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
        <p class="alert" v-if="errors.has('skill')"> {{ errors.first('skill') }}</p>
      </transition>
    </form>

    <ul>
      <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
        <li v-for="(data, index) in skills" v-bind:key=index+0> 
          {{ data.skill }}
          <i class="fa-fa-minus-circle" v-on:click="remove(index)">d</i>
        </li>
      </transition-group>
    </ul>

    <p v-if="skills.length == 0">Your skill set is currently empty</p>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data() {
    return {
      name: 'Teednet',
      skill: '',
      skills: [
        {'skill': 'Web design'},
        {'skill': 'Mobile Application'}
      ]
    }
  },

  methods: {
    addSkill() {
      this.$validator.validateAll().then((result) => {
        if(result){
          this.skills.push({'skill': this.skill});
          this.skill = '';
        }
      })
    },
    remove(id) {
      this.skills.splice(id, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
  @import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css"

  .skills {
    background: #fff
  }
  
  i {
    float: right;
    cursor: pointer;
  }

  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }

  ul li {
    padding: 20px;
    font-size: 1.0em;
    background-color: #e0edf4;
    border-left: 5px solid #3eb3f6;
    margin-bottom: 2px;;
    color: #3e5252;
  }

  p {
    text-align: center;
    padding: 30px 0;
    color: gray;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }

  input {
    width: calc(100% - 40px);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #323333;
    color: #687f7f;
  }

  .alert {
    background: #fdf2ce;
    font-wigth: bold;
    display: inline-block;
    padding: 5px;
    margin-top: -20px;
  }
</style>
