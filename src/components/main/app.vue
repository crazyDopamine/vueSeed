<template>
  <div id="app">
    <router-view :key="key"></router-view>
  </div>
</template>
<script type="es6">
  import router from '../../mainRouter'
  import {cookie} from 'vux'
  export default {
    router,
    computed: {
      key() {
        return this.$route.name !== undefined ? this.$route.name + new Date() : this.$route + new Date()
      }
    },
    data: function () {
      return {}
    },
    methods: {
      getUserInfo: function () {
        this.$http.get('user/selectUserInfo').then((rsp) => {
          this.userInfo = rsp.data
          this.userInfoLoaded = 1
          this.$emit(this.consts.loadedEvent, rsp.data)
        })
      }
    },
    created: function () {
      window.vm = this;
      var ticket = cookie.get(this.consts.ticketKey)
      if (ticket) {
        // this.getUserInfo()
      }
      router.afterEach(route => {
        document.body.scrollTop = 0
        document.documentElement.scrollTop = 0
      })
    }
  }
</script>
