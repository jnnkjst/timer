<template>
  <div>
    <h1>Item</h1>
    {{ countdown }}
  </div>
</template>
<script>
export default {
  props: { id: Number, countdown: Number },
  data() {
    return {
      c: 90,
    };
  },
};
</script>