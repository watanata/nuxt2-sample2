<template>
  <div>
    <div class="box">
      <div class="vul">
        <input type="text" name="mail" v-bind:value="value">
        <p>
          属性値を引用符で囲まない場合の脆弱性.Vue.jsではv-bindで変数を展開するため、引用符で囲まない書き方ができない。
        </p>
      </div>
      <div class="vul">
        <input type="text" name="sample" v-bind:value="value2">
        <p>
          引用符で囲んだ場合もダブルクォートのエスケープを自動的にやっているため、脆弱性を埋め込めない。
        </p>
      </div>
    </div>
    <div class="box">
      <div class="vul">
        <a v-bind:href="link">リンク</a>
        <p>ユーザーからの入力をそのままhref属性に適用するとjavascriptを実行可能</p>
        <p>対策はリンク先のホストをサーバー側で限定することとスキームをhttps, httpに限定することも有効</p>
      </div>
      <div class="vul">
        <a v-if="link.match(/^https?/)" v-bind:href="link">リンク</a>
        <p>対策：aタグに対してv-if="link.match(/^https?/)" でプロトコルを限定しているため、aタグ自体が表示されない</p>
      </div>
      <div class="vul">
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

body {
  font-family: sans-serif;
  background-color: #f7fafa;
}

input {
  width: 500px;
  height: auto;
  border: solid 1px #999;
}

.vul {
  margin: 5px;
  border-bottom: solid 1px #999;
}

.box {
  width: 940px;
  margin: 10px auto;
  padding: 0 10px;
  border: solid 1px #999;
  border-top: solid 7px #ed6103;
  border-radius: 5px;
  background-color: #ffff;
}
</style>
