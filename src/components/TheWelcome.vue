<script setup>
import WelcomeItem from './WelcomeItem.vue'
import ToolingIcon from './icons/IconTooling.vue'
import SupportIcon from './icons/IconSupport.vue'
</script>

<template>
  <WelcomeItem>
    <template #icon>
      <SupportIcon />
    </template>
    <template #heading><span class="green">Your HTTP Headers</span></template>
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <ToolingIcon />
    </template>
    <template #heading>
      <span>
        <ul v-for="head of heads">
          <li>
            <span class="green">{{ head.key }}: </span>
            <span>{{ head.value }}</span>
          </li>
        </ul>
      </span>
    </template>
  </WelcomeItem>
</template>

<script>
export default {
  props: {
    heads: {
      type: Array,
      default: [{key:"No HTTP Headers", value:"No HTTP Headers"}]
    }
  },
  methods: {
    getHeaders() {
      const req = new XMLHttpRequest();
      req.open('GET', "https://api.serginho.dev/headers", false);
      req.send(null);
      let json = JSON.parse(req.responseText);
      // json transform to array
      let heads = [];
      for (let key in json) {
        heads.push({key: key, value: json[key]});
      }
      return heads;
    }
  },
  computed: {
    heads() {
      return this.getHeaders()
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
</style>