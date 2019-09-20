<template>
  <div>
    <div>
      通常input要素のvalue属性などに直接ユーザーの入力を展開すると要素を書き換えられる脆弱性が入り込む。</br>
      しかし、Vue.jsではv-bindを使って属性値を注入するためデフォルトでHTMLエスケープされているのでv-bindを使えば同時に脆弱性対策になる。
    </div>
    <div>
      <p>粗大ごみ受付</p>
      <form action="" method="POST">
        氏名 <input name="name" v-bind:value="name"></br>
        品目 <input name="kind" v-bind:value="kind"></br>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData(context) {
    if (process.server) {
      context.res.setHeader("X-XSS-Protection","0")
      // return { value: context.req.body.value };
      return {
        name: context.req.body.name,
        kind: 'a-kind'
      };
    } else {
      return {
        name: '<span>hogehogehgoe</span>',
        kind: 'a-kind'
      };
    }
  }
};
</script>
