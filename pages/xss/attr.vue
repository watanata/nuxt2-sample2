<template>
  <div>
    <div v-html="name">
    </div>
    <div>
      <p>属性値を引用符で囲まない場合の脆弱性</p>
    </div>
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
