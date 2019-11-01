<template>
  <div>
    <header>
      <b-row class="navbar flex-md navbar-expand" align-v="center">
        <b-col cols="3">
          <b-img src="@/assets/images/bible.png" fluid width="20px"></b-img>
          <p class="category">&nbsp;Hebrew-English Bible</p>
        </b-col>
        <b-col cols="6" align-self="between">
          <fg-input
            addon-right-icon="now-ui-icons ui-1_zoom-bold"
            placeholder="Search Bible"
          >
          </fg-input>
        </b-col>
        <b-col align-self="end">
          <ul style="text-align: right">
            <li>Login | Register</li>
          </ul>
        </b-col>
      </b-row>
    </header>
  </div>
</template>
<script>
import { FormGroupInput } from '@/components'
export default {
  name: 'MainHeader',
  components: {
    [FormGroupInput.name]: FormGroupInput
  },
  data() {
    return {}
  }
}
</script>
<style></style>
