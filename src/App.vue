<template>
  <section class="todoapp">
    <section>
      <button @click="start">Start new Countdown</button>
      <Item
        v-for="it in items"
        :key="it.id"
        :id="it.id"
        :countdown="it.countdown"
      />
    </section>
  </section>
</template>

<script>
import Item from "./components/Item.vue";

export default {
  components: { Item },
  data() {
    return {
      items: [{ id: 0, countdown: 20 }],
      intervalId: "",
    };
  },
  mounted() {
    this.startInterval();
  },
  methods: {
    start() {
      this.items.push({ id: Math.random(), countdown: 20 });
      if (!this.intervalId) {
        this.startInterval();
      }
    },
    startInterval() {
      this.intervalId = setInterval(
        function () {
          this.items.forEach((element) => {
            element.countdown -= 1;
            if (element.countdown === 0) {
              this.remove(element.id);
            }
          });
        }.bind(this),
        1000
      );
    },
    remove(id) {
      const i = this.items.findIndex((el) => el.id === id);
      this.items.splice(i, 1);
      if (this.items.length === 1) {
        clearInterval(this.intervalId);
        this.intervalId = "";
      }
    },
  },
};
</script>
