<template>
  <div class="font-sans min-h-screen flex items-center justify-center">
    <div class="border-bevel m-2 shadow-shadow max-w-xl w-full text-brown-800">
      <div class="bg-paper shadow-bevel p-10 text-center">
        <h1 class="mb-4 text-2xl">
          Login
        </h1>
        <p v-if="formError" class="text-red-900 mb-2">
          {{ formError }}
        </p>
        <form autocomplete="off" @submit.prevent="login">
          <text-input
            class-name="mb-4"
            placeholder="Username"
            :value="formUsername"
            @input="formUsername = $event"
          />
          <password-input
            class-name="mb-4"
            placeholder="Password"
            :value="formPassword"
            @input="formPassword = $event"
          />
          <primary-button type="submit" class-name="mb-4">
            Login
          </primary-button>
          <NuxtLink to="/register">
            Create an account
          </NuxtLink>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import TextInput from '~/components/text-input.vue'
import PasswordInput from '~/components/password-input.vue'
import PrimaryButton from '~/components/primary-button.vue'
export default {
  name: 'Index',
  components: {
    TextInput,
    PasswordInput,
    PrimaryButton
  },
  data () {
    return {
      formError: null,
      formUsername: '',
      formPassword: ''
    }
  },
  methods: {
    async login () {
      try {
        await this.$store.dispatch('login', {
          username: this.formUsername,
          password: this.formPassword
        }).then(() => {
          this.formUsername = ''
          this.formPassword = ''
          this.formError = null
          this.$router.push({ path: '/story' })
        })
      } catch (e) {
        this.formError = e.message
      }
    }
    // async logout () {
    //   try {
    //     await this.$store.dispatch('logout')
    //   } catch (e) {
    //     this.formError = e.message
    //   }
    // }
  }
}
</script>
