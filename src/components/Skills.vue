<template>
  <div class="hello">
    <div class="container">
      <div class="holder">
        <form @submit.prevent="addSkill">
          <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
            <input type="text" placeholder="Enter a todo" v-model="skill" v-validate="'min:5'" name="skill">
            
          </transition>
        </form>
        <transition name="alert-in" enter-active-class="animated bounceIn" leave-active-class="animated bounceOut">
          {{ skill }}
          <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
        </transition>
      
    
      <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li v-for="(data, index) in skills" :key="index">{{ data.skill }}
            <i class="fa fa-minus-circle" v-on:click="remove(index)"></i>
          </li>
        </transition-group>
      </ul>

      <p>These are the skills that you possess.</p>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "skills",
  props: {
    
  },
  data(){
    return{
      skill: '',
      skills:[
        // {"skill": "Vue.js"},
        // {"skill": "Frontend Developer"}
      ]
    }
  },methods:{
    addSkill(){
      this.$validator.validateAll().then((result) => {
        if(result){
          this.skills.push({skill: this.skill})
          this.skill = '';
        }else{
          console.log('Not valid');
        }
      })
    },
    remove(id){
      this.skills.splice(id, 1);
    }
  },mounted(){
    this.$nextTick(() => {
      
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.holder{
  background: #fff;
}
ul{
  margin: 0;
  padding: 0;
  list-style-type: none;
  text-align: justify;
}
ul li{
  padding: 20px;
  font-size: 1.3em;
  background: #e0edf4;
  border-left: 5px solid #3eb3f6;
  margin-bottom: 2px;
  color: #3e5252;
}
p{
  text-align: center;
  padding: 30px 0;
  color: gray;
}
.container{
  box-shadow: 0px 0px 40px lightgray;
}
input{
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background: #323333;
  color: #687f7f;
}
.fa{
  float: right;
}
</style>
