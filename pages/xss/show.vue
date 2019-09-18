<template>
  <div>
    <div v-html="name">
    </div>
    <div>
      <p>このページはnameパラメータをそのままHTMLとして出力します</p>
    </div>
    <div>
      <p>対策："&lt;"と"&amp;"をエスケープする。</p>
      <p>または、vue.jsの場合はv-htmlを使わずに{{ }}のmustash記法などを用いる。下記はmustash記法を用いたもの</p>
      <div>
        {{ name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData(context) {
    if(process.server) {
      context.res.setHeader("X-XSS-Protection","0")
    }
    const escaped = escape(context.query.name)
    console.log(escaped)
    return {
      name: context.query.name,
      escaped: escaped
    };
  }
};
</script>
