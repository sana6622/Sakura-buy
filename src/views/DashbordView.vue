<template>
  <div>
    我是判斷有沒有登錄的畫面，
    看到我就表示有登錄了呦
  </div>
  <navbar></navbar>

<router-view/>
</template>

<script>
import Navbar from '@/components/NavbarList.vue'

export default {
  components: {
    Navbar
  },
  created () {
    const findToken = document.cookie.replace(/(?:(?:^|.*;\s*)getToken\s*=\s*([^;]*).*$)|^.*$/, '$1')
    console.log(findToken)
    this.$http.defaults.headers.common.Authorization = findToken
    const api = `${process.env.VUE_APP_API}api/user/check`
    this.$http.post(api)
      .then((res) => {
        if (!res.data.success) {
          this.$router.push('./login')
        }
        console.log(res)
      })
  }
}
</script>
