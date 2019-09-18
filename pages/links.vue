<template>
  <div>
    <ul>
      <li>
        <nuxt-link to='/xss/show?name=<img%20src%3D"hoge"%20onerror%3Dalert%281%29>'>DOM-Based-XSS</nuxt-link>
      </li>
      <li>
        <nuxt-link to='/xss/show?name=<img src="hoge" onerror=alert(1)>'>DOM-Based-XSS 2</nuxt-link>
      </li>
      <li>
        <nuxt-link to='/xss/show?name=<img src="hoge" onerror=alert(document.cookie)>'>DOM-Based-XSS 3</nuxt-link>
      </li>
      <li>
        <p>リンクを動的に生成する場合の脆弱性 linkパラメータ</p>
        <p>属性値を引用符で囲まない場合の脆弱性 valueパラメータ</p>
        <p>属性値を引用符で囲んだ場合の脆弱性 value2パラメータ</p>
        <nuxt-link to='/xss/attr?link=javascript%3Aalert%28document.cookie%29&value=1%20onmouseover%3Dalert%28document.cookie%29&value2="%20onmouseover%3D"alert%28document.cookie%29'>/xss/attr?link=javascript%3Aalert%28document.cookie%29&value=1%20onmouseover%3Dalert%28document.cookie%29&value2="%20onmouseover%3D"alert%28document.cookie%29</nuxt-link>
      </li>
    </ul>
  </div>
</template>
