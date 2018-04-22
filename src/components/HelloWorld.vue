<template>
  <div class="hello">
    <p>ユーザー名</p>
    <input v-model="name" type="text">
    <p>パスワード</p>
    <input v-model="pass" type="text">
    <br>
    <button v-on:click="check">チェック！！</button>
    <p>{{ result }}</p>
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  data () {
    return {
      name: '',
      pass: '',
      result: 'ここに結果が出るはずよ！'
    }
  },
  methods: {
    check () {
      var Instagram = require('instagram-private-api').V1
      var device = new Instagram.Device('someuser')
      var storage = new Instagram.CookieMemoryStorage()

      Instagram.Session.create(device, storage, this.name, this.pass)
        .then(function (session) { // username,passwordから利用者のaccountIDを特定
          return [session, Instagram.Account.searchForUser(session, name)]
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
p {
  color: #42b983;
}
</style>
