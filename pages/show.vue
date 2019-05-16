<template>
  <div v-html="name">
  </div>
</template>

<script>
export default {
  async asyncData(context) {
    if(process.server) {
      context.res.setHeader("X-XSS-Protection","0")
    }
    return { name: context.query.name };
  }
};
</script>
