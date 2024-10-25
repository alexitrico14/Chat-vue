<script>
export default {
  props: ['user'],  data() {
    return {
      message: '',
      messageColor: '#38aa1b',
    };
  },
  methods: {
    sendMessage() {
      this.$emit('message-sent', { text: this.message, color: this.messageColor });
      this.message = '';
    },
  },
};
</script>
<template>
  <div id="user1">
    <img :src="user.picture.large" alt="User picture" />
    <h2>{{ user.name.first }} {{ user.name.last }}</h2>
    <label for="colorPicker">Selecciona el color de tus mensajes:</label>
    <input type="color" v-model="messageColor" id="colorPicker" />
    <textarea v-model="message" placeholder="Escribe tu mensaje..."></textarea>

    <button @click="sendMessage">Enviar</button>
  </div>
</template>


<style scoped>
#user1 {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}

img {
  border-radius: 50%;
  width: 150px;
  height: 150px;
}

textarea {
  width: 100%;
  height: 100px;
  margin: 10px 0;
}

button {
  padding: 10px 20px;
  cursor: pointer;
}
</style>