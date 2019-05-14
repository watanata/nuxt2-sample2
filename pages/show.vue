<template>
</template>

<script>
export default {
  async asyncData(context) {
    console.log('context.query');
    console.log(context.query);
    console.log('context.params');
    console.log(context.params);
  }
};
</script>
