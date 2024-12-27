<script>
import axios from 'axios';
import ChatBox from './components/ChatBox.vue';

export default{
  name: "App",
  data(){
    return{
      message:[],
      personaLeft:{
        nombre: "",
        direction: "left",
        src: "",
        input: "",
        color: "",
      },
      personaRight: {
        nombre:"",
        direction:"right",
        src:"",
        input:"",
        color:"",
      },
      };
    },
    methods: {
      addMessage(persona) {
        this.messages.push({ ...persona });
      },

      async getPersonas() {
        const url = "https://randomuser.me/api?results=2";
        const { data } = await axios.get(url);
        this.personaLeft.nombre = 
        data.results[0].name.first + " " + data.results[0].name.last;
        this.personaLeft.src = data.results[0].picture.large;
        this.personaRight.nombre =
        data.results[1].name.first + " " + data.results[1].name.last;
        this.personaRight.src = data.results[1].picture.large;
      },
    },
    mounted() {
      this.getPersonas();
    },
    components: {
      ChatBox,
    },
  };

</script>

<template>
  <div id="app">
    <router-view />
    <div class="persona p-1">
      <img :src="personaLeft.src" />
<span>{{ personaLeft.nombre }}</span>
<input v-model="personaLeft.color" type="color"/>
<textarea v-model="personaLeft.Input" rows="8"></textarea>
<button @click="addMessage(personaLeft)">enviar</button>
    </div>

    <ChatBox :messages="messages" @hideMessage="hideMessage" />
  
  <div class="persona p-2">
    <img :src="personaRight.src"/>
    <span style="text-align: right;"> {{ personaRight.nombre }} </span>
    <input v-model="personaRight.color" type="color"/>
    <textarea v-model="personaRight.Input" rows="8"></textarea>
    <button @click="addMessage(personaRight)">enviar</button>
</div>
  </div>
</template>

<style lang="scss">
*{ 
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  grid-template-columns: 200px 400px 200px;
  padding: 20px;
  gap: 15px;
}
.persona{
  display: flex;
  flex-direction: column;
  input{
    width: 100%;
  }
  gap: 5px;
}
</style>
