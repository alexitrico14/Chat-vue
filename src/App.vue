<script>
import axios from 'axios';
import UserInput from './components/UserInput.vue';
import Message from './components/Message.vue';

export default {
  data() {
    return {
      user1: null,
      user2: null,
      gender1: 'male',
      gender2: 'female',
      messages: []
    };
  },
  async mounted() {
    await this.fetchUser1();
    await this.fetchUser2();
  },
  methods: {
    async fetchUser1() {
      try {
        const url = `https://randomuser.me/api/?gender=${this.gender1}`;
        const { data } = await axios.get(url);
        this.user1 = data.results;
      } catch (error) {
        console.error("Error al obtener el usuario 1", error);
      }
    },
    async fetchUser2() {
      try {
        const url = `https://randomuser.me/api/?gender=${this.gender2}`;
        const { data } = await axios.get(url);
        this.user2 = data.results;
      } catch (error) {
        console.error("Error al obtener el usuario 2", error);
      }
    },
    handleMessage1(message) {
      const newMessage = {
        text: message.text,
        color: message.color,
        sender: this.user1[0].name.first
      };
      this.messages.push(newMessage);
    },
    handleMessage2(message) {
      const newMessage = {
        text: message.text,
        color: message.color,
        sender: this.user2[0].name.first
      };
      this.messages.push(newMessage);
    }
  },
  components: {
    UserInput,
    Message
  }
};
</script>

<template>
  <div id="App" class="container">
    <div class="row">
      <div class="col-3 user-section">
        <UserInput v-if="user2" :user="user2[0]" @message-sent="handleMessage2" />
      </div>

      <div class="col-6 chat-section">
        <div class="messages">
          <Message v-for="(msg, index) in messages" :key="index" :message="msg"
            :isSentByUser="user1 && msg.sender === user1[0].name.first" />
        </div>
      </div>

      <div class="col-3 user-section">
        <UserInput v-if="user1" :user="user1[0]" @message-sent="handleMessage1" />
      </div>
    </div>
  </div>
</template>


<style scoped>
/* Estilos generales */
.container {
  margin-top: 20px;
}

.row {
  display: flex;
  justify-content: space-between;
  gap: 20px;
}

.col-3 {
  width: 25%;
}

.col-6 {
  width: 50%;
}

/* Sección de usuario */
.user-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #b2dfaa;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.1);
}

img {
  border-radius: 50%;
  width: 150px;
  height: 150px;
}

/* Selector de color y botón */
input[type="color"] {
  margin-top: 10px;
  width: 50px;
  height: 30px;
  border: none;
  cursor: pointer;
}

button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 10px;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #0056b3;
}

/* Sección de mensajes */
.chat-section {
  background-image: url('../src/assets/img/background-wsp.png');
  background-size: cover;
  background-color: #ffffff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.1);
  height: 500px;
  overflow-y: scroll;
}

.messages {
  display: flex;
  flex-direction: column;
}
</style>
