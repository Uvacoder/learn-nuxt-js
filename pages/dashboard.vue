<template>
  <div>
    <Navigation />
    <header class="bg-white shadow">
      <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
        <h1 class="text-3xl font-bold leading-tight text-gray-900">Dashboard</h1>
      </div>
    </header>
    <main>
      <div class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">

      </div>
    </main>
  </div>
</template>

<script>
  import Navigation from '~/components/main/Navigation.vue'
  export default {
    components: {
      Navigation
    },
    data() {
      return {
        ip: ''
      }
    },
    mounted(){
      console.log(this.$auth.loggedIn)
      this.fetchSomething()
    },
    methods: {
      async fetchSomething() {
        const ip = await this.$axios.$get('http://icanhazip.com')
        this.ip = ip
      }
    }
  }

</script>
