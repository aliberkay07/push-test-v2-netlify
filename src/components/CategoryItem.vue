<template>
  <div :class="{ [category.class]: true }">
    <span>
      <i :class="{ [category.icon]: true }" class="fab fa-2x"></i>
      <span>{{ category.title }} - {{ category.id}}</span>
    </span>
    <button @click="takip">Takip Et!</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  props: ["category"],
  data(){
    return {
      serviceWorker : null
    }
  },
  methods: {
    async takip() {
      this.serviceWorker = await navigator.serviceWorker.ready;
      const cliendId = await this.serviceWorker.pushManager.subscribe({
        userVisibleOnly : true,
        applicationServerKey: "BAJofqCfr_ztf2ZXJYa7rz1XEjEirEKgP1dJ9Mln5PslYR-eJhnTLALWYaZyHrTMxTiYr7uakXQvZ-WxOr40Q2M"
      });
      axios.post(`http://localhost:3000/subscribe/${this.category.id}`,{
        subscriber : cliendId
      }).then((category_sub_response) => {
        console.log('category_sub_response :>>', category_sub_response);
      })
    }
  },
  async created() {
      this.serviceWorker = await navigator.serviceWorker.register("./sw.js");
  }
}
</script>