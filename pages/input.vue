<template>
  <div>
    <div>
      <p>粗大ごみ受付</p>
      <form action="" method="POST">
        氏名 <input v-html="name">
      </form>
    </div>
    <div>
      上記のInput要素にはvalueに直接ユーザーの入力を展開するため要素を書き換えられる脆弱性があります。</br>
      しかし、Vue.jsがrawHtml内の閉じタグによって上位のタグを閉じない様になっている（脆弱性対策？）ためinput要素の子要素として外部からタグが注入される。
    </div>
  </div>
</template>

<script>
export default {
  async asyncData(context) {
    if (process.server) {
      context.res.setHeader("X-XSS-Protection","0")
      return { name: context.req.body.name };
    } else {
      return {name: 'foobar'}
    }
  }
};
</script>
