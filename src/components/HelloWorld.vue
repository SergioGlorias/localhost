<script setup>
import axios from 'axios'
</script>

<template>

  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>{{ ip }}</h3>
  </div>

</template>

<script>
export default {
  data() {
    return {
      msg: "Your IP",
      ip: "Unknown"
    };
  },
  methods: {
    getIP() {
      const req = new XMLHttpRequest();
      req.open('GET', "/cdn-cgi/trace", false);
      req.send(null);
      // is paintext, but works
      let ip = req.responseText.split("\n")
      ip = ip.filter((data) => data.startsWith("ip="))
      ip = ip[0].replace("ip=", "")
      return ip;
    }
  },
  mounted() {
    this.ip = this.getIP();
  }
}

</script>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;

}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {

  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
