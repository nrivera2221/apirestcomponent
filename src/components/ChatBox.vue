<script>
export default {
  props: ['messages'],
};
</script>

<template>
  <div class="chat-box">
    <div
      v-for="({ input, color, direction, nombre }, i) in messages"
      :key="i"
      :class="{ left: direction == 'left', right: direction == 'right' }">
      <span class="nombre">{{ nombre }}</span>
      <p @click="$emit('hideMessage')" :style="{backgroundColor: color}" class="message">
      <span> {{ input }} </span>
      </p>
    </div>
  </div>
</template>


<style lang="scss">
.chat-box {
  height: 400px;
  width: 400px;
  overflow-y: scroll;
  border: 1px solid #ccc;
  padding: 10px 15px;
  background-color: #eee7dd;
box-shadow: 0px 0px 4px 1px #591f1f;
max-height: 417px;
.nombre{
  font-size: 0.7rem;
  color: grey;
}
>div {
  display: flex;
  flex-direction: column;
}
}
.left{
  align-self: flex-start;
  text-align: left;
  align-items: flex-start;
}
.right{
  align-self: flex-start;
  text-align: left;
  align-items: flex-end;
}
.message {
  margin: 5px 0px;
  padding: 5px 10px;
  border-radius: 20px;
  width: fit-content;
  i{
    font-style: normal;
    font-size: 0.7rem;
    cursor: pointer;
  }
}
.p-1 {
  text-align: left;
}
.p-2 {
  text-align: right;
}
</style>
