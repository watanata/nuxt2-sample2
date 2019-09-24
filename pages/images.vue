<template>
  <div>
    <ul>
      <li
         v-for="(url, index) in images"
         :key="index"
       >
        <div class="box">
          <h2>sample title</h2>
          <div class="spec">
            <div class="left-spec">
              <no-ssr>
                <lazy-component>
                  <img
                    :src="url"
                   width="400"
                   class="property-image"
                 >
                </lazy-component>
              </no-ssr>
            </div>
            <div class="right-spec">
              <table>
                <tbody>
                  <tr>
                    <th>aaa</th>
                    <td>bbb</td>
                  </tr>
                  <tr>
                    <th>cccc</th>
                    <td>ddd</td>
                  </tr>
                  <tr>
                    <th>hoge</th>
                    <td>moge</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
 </template>

<script>
import axios from '~/plugins/axios';

export default {
  async asyncData() {
    let result;
    try {
      result = await axios.get('/api/images');
    } catch (err) {
      console.log(err);
    }
    return { images: result.data };
  }
};
</script>


<style>

body {
  background-color: #f7fafa;
}

ol, ul {
  list-style: none;
}

.property-image {
  margin: 10px;
  max-width: 208px;
  max-height: 138px;
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

/* ブロック要素を横に並べる */
.box div {
  display: inline-block;
}

/* 左寄せ */
.left-spec {
  float: left;
}

/* reset default table style */
table {
  border-collapse: collapse;
  border-spacing: 0;
}

th, td {
  border: 1px solid #bdc8ca;
}

th {
  width: 25%;
}

td {
  width: 75%;
}

.spec {
  width: 100%;
}

</style>
