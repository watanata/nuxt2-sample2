<template>
  <div>
    <p>粗大ごみ受付</p>
    <form action="" method="POST">
      氏名 <input type="text" name="name" v-bind:value="name" >
    </form>
  </div>
</template>

<script>
export default {
  async asyncData(context) {
    console.log('hogehgoehgeohgeohgoeh')
    context.res.setHeader("X-XSS-Protection","0")
    return { name: context.params.name };
  }
};
</script>
