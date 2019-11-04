<template>
  <div class="header">
    <i class="fa fa-bars"></i>
    <div class="setting-wrapper">
        <div class="setting-container">
          <span>종료시간</span>
          <input type="text">
        </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Settings',
  data () {
    return {
      date: ''
    }
  }
}
</script>

<style scoped>
.header {
  position: absolute;
  padding: 20px;
  top: 0;
  right: 0;
}

.setting-wrapper {
  position: absolute;
  right: 0;
  width: 500px;
  background-color: azure;
}

.setting-container {
  display: flex;
}

</style>
