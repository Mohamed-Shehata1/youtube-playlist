<template>
  <div id="app">
    <div class="header">
      <h1>Welcome To Youtube Playlist App</h1>
      <p>Today's Date Is  {{moment().format('DD MMM YYYY')}}</p>
    </div>
    <videos-list></videos-list>
  </div>
</template>

<script>
var moment = require('moment');
export default {
  data() {
    return {
      moment:moment
    }
  }
}
</script>

<style scoped>
.header {
  padding: 10px;
  background-color: #F9F9F9;
  font-size: 25px;
  color: #FE0303;
}
.header h1 {
  font-size: 50px;
  margin: 0 0 5px 10px;
}
.header p {
 margin: 5px 0px 10px 20px; 
 color: #d40e0e;
}

</style>