<template>
  <b-col cols xl="3" md="6" xs="12">
    <bulma-accordion initial-open-item="1">
      <bulma-accordion-item
        v-for="(reading, readingName) in bibleObj"
        :key="readingName"
      >
        <span slot="title" class="is-6 has-text-weight-normal">
          {{ readingName }}
        </span>
        <div slot="content" class="is-size-6">
          <li v-for="(book, bookName) in reading" :key="bookName">
            <n-link to="/">{{ bookName }}</n-link>
          </li>
        </div>
      </bulma-accordion-item>
    </bulma-accordion>
  </b-col>
</template>
<script>
import { BulmaAccordion, BulmaAccordionItem } from 'vue-bulma-accordion'
import demoBible from '@/assets/bible.json'
export default {
  name: 'Navbar',
  components: {
    BulmaAccordion,
    BulmaAccordionItem
  },
  data() {
    return {
      bibleObj: demoBible
    }
  }
}
</script>
<style>
.card-header {
  height: 50px;
}
.card-header-icon {
  width: 40px;
}
</style>
