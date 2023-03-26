<template>
  <div class="newTimer">
    <p>Добавить Таймер</p>
    <img class="add" src="@/assets/img/add.png" @click="createTimer" alt="Add">
  </div>
</template>

<script>
export default {
  methods: {
    createTimer() {
      this.$emit('create-timer')
    }
  }
}
</script>

<style scoped>
.newTimer{
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: flex-start;
  width: 100%;
  max-width: 225px;
  height: 120px;
  background: #696969;
  margin: 0 25px;
}

img{
  width: 20px;
  height: 20px;
  cursor: pointer;
}

p{
  color: #fff;
  font-size: 18px;
}

</style>