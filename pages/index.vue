<template>
  <b-container>
    <b-row align-h="center">
      <b-col cols="8">
        <div class="logo">
          <b-img src="@/assets/images/bible.png" center fluid></b-img>
          <h3 class="title">Hebrew-English Bible</h3>
          <p class="description">
            Read - Customize - Edit
          </p>
        </div>
        <div class="search">
          <fg-input
            addon-right-icon="now-ui-icons ui-1_zoom-bold"
            placeholder="Search Bible"
          >
          </fg-input>
        </div>
        <p class="category">Or Choose</p>
        <li v-for="(reading, name) in bibleObj" :key="name">
          {{ name }}
          <div class="readings">
            <n-link v-for="(torah, book) in reading" :key="book" to="/result">
              {{ book }} |
            </n-link>
          </div>
        </li>
      </b-col>
    </b-row>
  </b-container>
</template>
<script>
import demoBible from '@/assets/bible.json'
import { FormGroupInput } from '@/components'
export default {
  components: {
    [FormGroupInput.name]: FormGroupInput
  },
  data() {
    return {
      bibleObj: demoBible,
      selected: ''
    }
  }
}
</script>
<style>
.logo {
  color: #074852;
  text-align: center;
  margin-top: 20px;
}
li {
  list-style-type: none;
}
.search {
  margin-top: 30px;
}
.readings {
  align-items: center;
}
</style>
