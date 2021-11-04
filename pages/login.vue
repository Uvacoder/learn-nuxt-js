<template>
  <div>
    <Navigation />
    <header class="bg-white shadow">
      <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
        <h1 class="text-3xl font-bold leading-tight text-gray-900">Login</h1>
      </div>
    </header>
    <main>
      <div class="flex w-screen justify-center">
        <div class="w-1/2 mx-auto py-6 sm:px-6 lg:px-8">
          <Alert v-if="alert" :message="alert" />
          <div class="mt-5 rounded overflow-hidden shadow-lg">
            <div class="px-6 py-4 bg-gray-800">
              <div class="font-bold text-xl text-white">Login</div>
            </div>
            <form method="post" @submit.prevent="actionLogin">
              <div class="px-6 pb-2">
                <div class="mt-8 w-100">
                  <div class="grid grid-cols-1 gap-6">
                    <label class="block">
                      <span class="text-dark">Username</span>
                      <input v-model="username" type="text" class="mt-1 block w-full" placeholder="Username" />
                    </label>
                    <label class="block">
                      <span class="text-dark">Password</span>
                      <input v-model="password" type="password" class="mt-1 block w-full" placeholder="Password" />
                    </label>
                  </div>
                </div>
              </div>
              <div class="px-6 pt-4 pb-2">
                <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                  Submit
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
  // eslint-disable-next-line no-unused-vars
  import {
    mapMutations
  } from 'vuex'

  import Alert from '~/components/partials/Alert.vue'
  import Navigation from '~/components/main/Navigation.vue'

  export default {
    components: {
      Navigation,
      Alert,
    },
    auth: false,
    data() {
      return {
        username: null,
        password: null,
        alert: null,
      }
    },
    mounted() {
      if (this.$auth.loggedIn) {
          this.$router.push('/dashboard')
      }
    },
    methods: {
      ...mapMutations(['SET_IS_AUTH']),
      actionLogin() {
        this.$auth.loginWith('local', {
          data: {
            username: this.username,
            password: this.password
          }
        }).then((result) => {
          console.log(result)
          this.alert = null
          this.SET_IS_AUTH(true)
          this.$router.push('/dashboard')

        }).catch((err) => {
          this.alert = err.response.data.msg
        });
        // try {
        //   this.$auth.loginWith('local', {
        //     data: {
        //       username: this.username,
        //       password: this.password
        //     }
        //   })
        //   this.SET_IS_AUTH(true)
        //   this.$router.push('/')
        // } catch (e) {
        //   console.log(e);
        // }
      }
      // actionLogin: () => {
      //   this.$auth.loginWith('local', {
      //     data: {
      //       username: this.username,
      //       password: this.password
      //     }
      //   }).then(() => {
      //     // JIKA BERHASIL, KITA SET TRUE IS AUTH-NYA
      //     this.SET_IS_AUTH(true)
      //     // LALU REDIRECT KE HALAMAN UTAMA / DAHSBOARD
      //     this.$router.push('/')
      //   })
      // },
    }
  }

</script>
