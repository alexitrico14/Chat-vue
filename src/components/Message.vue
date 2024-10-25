<script>
export default {
  props: ['message', 'isSentByUser'],
};
</script>

<template>
  <div :class="['message', {'sent': isSentByUser}]">
    <div class="message-bubble" :style="{ backgroundColor: message.color || '#e5e5ea' }">
      <p>{{ message.text }}</p>
      <span class="message-info">{{ message.sender }}</span>
    </div>
    
  </div>
</template>

<style scoped>
.message {
  display: flex;
  justify-content: flex-start;
  margin: 15px 0;
  word-wrap: break-word;
}

.message.sent {
  justify-content: flex-end;
}

.message-bubble {
  background-color: #007bff;
  padding: 15px 20px;
  border-radius: 20px 20px 20px 20px;
  color: white;
  box-shadow: 2px 4px 10px rgba(0, 0, 0, 0.2);
  word-wrap: break-word;
  opacity: 0;
  animation: fadeIn 0.5s forwards;
}

@keyframes fadeIn {
  to {
    opacity: 1;
  }
}

.message p {
  margin: 0;
  font-size: 1em;
}

.message-info {
  display: block;
  font-size: 0.8em;
  font-style: italic;
  color: #000;
  margin-top: 5px;
  text-align: right;
}

.message.sent .message-bubble {
  background-color: #007bff;
}

.message.sent .message-info {
  color: #000;
}
</style>
