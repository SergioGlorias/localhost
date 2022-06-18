
<template>

  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>{{ ip }}</h3>
  </div>

</template>

<script>
export default {
  props: {
    msg: {
      type: String,
      default: 'Your IP'
    },
    ip: {
      type: String,
      default: "Unknown"
    }
  },
  methods: {
    getIP() {
      const req = new XMLHttpRequest();
      req.open('GET', "/cdn-cgi/trace", false);
      req.send(null);
      // is paintext, but works
      let ip = req.responseText.match(/[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}/);
      ip = ip ? ip[0] : "Unknown";
      return ip;
    }
  },
  computed: {
     ip() {
      return this.getIP()
    }
  },
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
