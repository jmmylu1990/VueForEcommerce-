<template>
  <NavBar></NavBar>
  <router-view/>
</template>
<script>

import NavBar from '../components/NavBar.vue';

export default {
  // 區域註冊
  components: {
    NavBar,
  },
  created() {
    // 取得儲存在瀏覽器，自定義名稱名為hexToken的token
    const token = document.cookie.replace(/(?:(?:^|.*;\s*)hexToken\s*=\s*([^;]*).*$)|^.*$/, '$1');
    console.log('進入dashboard');
    console.log(token);
    this.$http.defaults.headers.common.Authorization = token;
    const api = `${process.env.VUE_APP_API}/api/user/check`;
    this.$http.post(api).then((res) => {
      console.log(res);
      if (!res.data.success) {
        console.log('登入失敗');
        // this.$router.push('/login');
      }
    });
  },
};
</script>
