<script setup>
import WelcomeItem from "./WelcomeItem.vue";
import ToolingIcon from "./icons/IconTooling.vue";
import SupportIcon from "./icons/IconSupport.vue";
import axios from "axios";
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
  data() {
    return {
      heads: [{ key: "No HTTP Headers", value: "No HTTP Headers" }],
    };
  },
  methods: {
    getHeaders() {
      /*const req = fetch("https://api.serginho.dev/headers");
      let json = req.then(res => res.json()).then(json => json);
      // json transform to array
      let heads = [];
      for (let key in json) {
        heads.push({ key: key, value: json[key] });
      }
      return heads || [{ key: "No HTTP Headers", value: "No HTTP Headers" }];*/
      return axios.get("https://api.serginho.dev/headers").then((res) => {
        let heads = [];
        for (let key in res.data) {
          heads.push({ key: key, value: res.data[key] });
        }
        return heads || [{ key: "No HTTP Headers", value: "No HTTP Headers" }];
      });
    },
  },
  mounted() {
    this.getHeaders().then((heads) => {
      this.heads = heads;
    });
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
</style>
