<template>
  <v-container fluid class="mx-0 mt-n10 px-0 align-center justify-center fill-height overlay">
    <v-parallax
      height="700"
      cover
      class="hero1 align-center"
      src="/img/courtroom.png"
      lazy="/img/courtroom.png">
      <v-container>
        <v-row justify="center" align="center" class="">
          <v-col cols="xs-12 md-5" class="hero-text">
            <p class="text-overline">McKenzie Law, PLLC.</p>
            <h2 class="mb-3">We're here to defend you.</h2>
            <p class="mb-5">Our investigators and experts are not afraid to fight aggressively for your rights in court.</p>
            <v-btn prepend-icon="mdi-phone" variant="text" href="tel:4065774131">In a Mess? Call Wes!</v-btn>
          </v-col>
          <v-col offset="md-2" class="d-none d-md-block">
            <v-form name="heroContact" action="/thanks" method="POST" data-netlify="true">
              <input type="hidden" name="form-name" value="heroContact" />
              <v-text-field
                variant="outlined"
                v-model="name.value.value"
                :counter="40"
                :error-messages="name.errorMessage.value"
                label="Name"></v-text-field>

              <v-text-field
                variant="outlined"
                v-model="phone.value.value"
                :counter="10"
                :error-messages="phone.errorMessage.value"
                label="Phone Number"></v-text-field>

              <v-text-field
                variant="outlined"
                v-model="email.value.value"
                :error-messages="email.errorMessage.value"
                label="E-mail"></v-text-field>

              <v-select
                variant="outlined"
                v-model="select.value.value"
                :items="items"
                :error-messages="select.errorMessage.value"
                label="Consult Type"></v-select>

              <v-btn
                class="me-4"
                type="submit"
                color="light-blue-accent-3"
                flat
                >
                submit
              </v-btn>

              <v-btn @click="handleReset" variant="text" color="deep-orange-darken-1">
                clear
              </v-btn>
            </v-form>
          </v-col>
        </v-row>
      </v-container>
    </v-parallax>
  </v-container>
</template>

<style lang="scss">
.hero1 {
  font-family: "Inter";
  color: white;
  text-shadow: 0 2px 10px rgba(0, 0, 0, .4);

  h2 {
    font-weight: 700;
    line-height: 1.2;
    font-size: 3.5em;
  }

  p {
    font-size: 1.25em;
    font-weight: 400;
  }
}
</style>

<script>
import { ref } from 'vue'
import { useField, useForm } from 'vee-validate'
// import AboutBlock from '../sections/AboutBlock.vue'

export default {
  setup() {
    const { handleSubmit, handleReset } = useForm({
      validationSchema: {
        name(value) {
          if (value?.length >= 2) return true

          return 'Name needs to be at least 2 characters.'
        },
        phone(value) {
          if (value?.length > 9 && /[0-9-]+/.test(value)) return true

          return 'Phone number needs to be at least 9 digits.'
        },
        email(value) {
          if (/^[a-z.-]+@[a-z.-]+\.[a-z]+$/i.test(value)) return true

          return 'Must be a valid e-mail.'
        },
        select(value) {
          if (value) return true

          return 'Select an item.'
        },
      },
    })
    const name = useField('name')
    const phone = useField('phone')
    const email = useField('email')
    const select = useField('select')

    const items = ref([
      'Consultation',
      'Non-Violent Offense',
      'Violent Offense',
      'Appeals'
    ])

    const submit = () => {
      handleSubmit();
      alert("Your form has been submitted.");
    };

    return { name, phone, email, select, items, submit, handleReset }
  },
}
</script>