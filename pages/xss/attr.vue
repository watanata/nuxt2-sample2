<template>
  <div>
    <div class="box">
      <div>
        <input type="text" name="mail" v-bind:value="value">
      </div>
      <div>
        <input type="text" name="sample" v-bind:value="value2">
      </div>
      <div>
        <p>
          属性値を引用符で囲まない場合の脆弱性.Vue.jsではv-bindで変数を展開するため、引用符で囲まない書き方ができない。
        </p>
        <p>
          引用符で囲んだ場合もダブルクォートのエスケープを自動的にやっているため、脆弱性を埋め込めない。
        </p>
      </div>
    </div>
    <div class="box">
      <div>
        <a v-bind:href="link">リンク</a>
        <p>ユーザーからの入力をそのままhref属性に適用するとjavascriptを実行可能</p>
        <p>対策はリンク先のホストをサーバー側で限定することとスキームをhttps, httpに限定することも有効</p>
      </div>
      <div>
        <a v-if="link.match(/^https?/)" v-bind:href="link">リンク</a>
        <p>対策：aタグに対してv-if="link.match(/^https?/)" でプロトコルを限定</p>
      </div>
      <div>
        <nuxt-link v-bind:to="link">nuxt-linkで生成したリンク</nuxt-link>
        <p>相対URLを作成するためjavascript式は実行されない</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData(context) {
    if(process.server) {
      context.res.setHeader("X-XSS-Protection","0")
      console.log(context.res)
    }
    return {
      value: context.query.value,
      value2: context.query.value2,
      link: context.query.link,
      raw: context.query.raw
    };
  }
};
</script>

<style>
.box {
  border: 1px solid;
}
</style>
