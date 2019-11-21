<template>
  <b-container>
    <b-row>
      <b-breadcrumb :items="items"></b-breadcrumb>
      <b-col cols="12">
        <b-row>
          <b-dd text="Chapter">
            <b-dropdown-item
              v-for="(chapter, name) in bibleObj.Torah.Genesis"
              :key="name"
            >
              {{ name + 1 }}
            </b-dropdown-item>
          </b-dd>
        </b-row>
        <b-row align-h="end">
          <n-checkbox v-model="lang.eng">Eng &nbsp;</n-checkbox>
          <n-checkbox v-model="lang.heb">עברית</n-checkbox>
        </b-row>
        <b-row align-h="end">
          <n-button simple icon size="sm">
            <i
              v-b-tooltip.hover
              title="Color Palette"
              placement="bottom"
              class="now-ui-icons design_palette"
              @click="modals.palette = !modals.palette"
            ></i>
          </n-button>
        </b-row>
        <b-row>
          <b-col v-if="lang.heb">
            <h3 class="heb">בְּרֵאשִׁית</h3>
          </b-col>
          <b-col v-if="lang.eng">
            <h3>Genesis</h3>
          </b-col>
        </b-row>
        <table class="table">
          <thead>
            <tr>
              <th v-if="lang.heb">
                <h5 class="heb">1 פרק</h5>
              </th>
              <th v-if="lang.eng">
                <h5>Chapter 1</h5>
              </th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(verse, index) in bibleObj.Torah.Genesis[0]"
              :key="index"
            >
              <td v-if="lang.heb" class="heb">
                <span
                  v-if="customize[index].icon && !customize[index].edit"
                  class="float-left"
                >
                  <i
                    v-b-tooltip.hover
                    title="Edit Verse"
                    class="fas fa-sm fa-edit"
                    @click="editVerse($event, index)"
                  ></i>
                  <i
                    v-b-tooltip.hover
                    title="Apply Color"
                    class="fas fa-sm fa-fill-drip"
                    @click="applyColor($event, index)"
                  ></i>
                  <i
                    v-b-tooltip.hover
                    title="Show Value"
                    class="fas fa-sm fa-info"
                    @click="applyValue($event, index)"
                  ></i>
                </span>
                <span>
                  <i
                    v-if="!customize[index].icon && !customize[index].edit"
                    v-b-tooltip.hover
                    title="Options"
                    class="fas fa-sm fa-ellipsis-h float-left"
                    @click="showCustomizeOption($event, index)"
                  ></i>
                </span>
                <span v-if="!customize[index].edit" ref="verse">{{
                  toHeb(index + 1) + '. ' + verse.he
                }}</span>
                <b-textarea
                  v-if="customize[index].edit"
                  v-model="verse.he"
                  size="sm"
                ></b-textarea>
                <a
                  v-show="customize[index].edit"
                  href
                  class="float-left"
                  @click="customize[index].edit = !customize[index].edit"
                  >לשמור</a
                >
              </td>
              <td v-if="lang.eng">
                <span v-if="!customize[index].edit">{{
                  index + 1 + '. ' + verse.eng
                }}</span>
                <b-textarea
                  v-if="customize[index].edit"
                  v-model="verse.eng"
                  size="sm"
                ></b-textarea>
                <a
                  v-show="customize[index].edit"
                  class="float-right"
                  @click="customize[index].edit = !customize[index].edit"
                  >Save</a
                >
              </td>
            </tr>
          </tbody>
        </table>
      </b-col>
    </b-row>
    <!-- <modal :show.sync="modals.palette" header-classes="justify-content-center">
      <b-container>
        <h5 slot="header">Assign Colors</h5>
        <b-row>
          <b-col v-for="(letter, key) in hebLetterMap" :key="key">
            &nbsp;&nbsp;{{ letter.letter }}
            <swatches
              v-model="letter.col"
              colors="text-advanced"
              popover-to="right"
              :trigger-style="{ width: '30px', height: '30px' }"
            ></swatches>
          </b-col>
        </b-row>

        <span slot="footer">
          <n-button type="success-outline" @click="modals.palette = !modals.palette">Save</n-button>
          <n-button type="danger" @click="modals.palette = !modals.palette">Close</n-button>
        </span>
      </b-container>
    </modal>-->
  </b-container>
</template>
<script>
import 'vue-swatches/dist/vue-swatches.min.css'
import { Checkbox, FormGroupInput, Button } from '@/components'
import demoBible from '@/assets/bible.json'
export default {
  layout: 'reading',
  name: 'Result',
  components: {
    [Button.name]: Button,
    [Checkbox.name]: Checkbox,
    [FormGroupInput.name]: FormGroupInput
  },

  data() {
    return {
      bibleObj: demoBible,
      lang: {
        eng: true,
        heb: true
      },
      modals: {
        palette: false
      },
      items: [
        {
          text: 'Genesis',
          active: true
        },
        {
          text: 'Exodus',
          href: '#'
        },
        {
          text: 'Leviticus',
          href: '#'
        },
        {
          text: 'Numbers',
          href: '#'
        },
        {
          text: 'Deuteronomy',
          href: '#'
        }
      ],
      customize: [
        { icon: false, edit: false, color: false, value: false },
        { icon: false, edit: false, color: false, value: false },
        { icon: false, edit: false, color: false, value: false },
        { icon: false, edit: false, color: false, value: false },
        { icon: false, edit: false, color: false, value: false },
        { icon: false, edit: false, color: false, value: false },
        { icon: false, edit: false, color: false, value: false },
        { icon: false, edit: false, color: false, value: false },
        { icon: false, edit: false, color: false, value: false },
        { icon: false, edit: false, color: false, value: false }
      ],
      map: {
        0: '-',
        1: 'א',
        2: 'ב',
        3: 'ג',
        4: 'ד',
        5: 'ה',
        6: 'ו',
        7: 'ז',
        8: 'ח',
        9: 'ט',
        10: 'י'
      },
      hebLetterMap: {
        א: { val: 1, col: '#000000' },
        בּ: { val: 2, col: '#000000' },
        ב: { val: 2, col: '#000000' },
        ג: { val: 3, col: '#000000' },
        ד: { val: 4, col: '#000000' },
        ה: { val: 5, col: '#000000' },
        ו: { val: 6, col: '#000000' },
        ז: { val: 7, col: '#000000' },
        ח: { val: 8, col: '#000000' },
        ט: { val: 9, col: '#000000' },
        י: { val: 10, col: '#000000' },
        כּ: { val: 20, col: '#000000' },
        כ: { val: 20, col: '#000000' },
        ךּ: { val: 30, col: '#000000' },
        ך: { val: 30, col: '#000000' },
        ל: { val: 30, col: '#000000' },
        מ: { val: 40, col: '#000000' },
        ם: { val: 600, col: '#000000' },
        נ: { val: 50, col: '#000000' },
        ן: { val: 500, col: '#000000' },
        ס: { val: 60, col: '#000000' },
        ע: { val: 70, col: '#000000' },
        פּ: { val: 80, col: '#000000' },
        ף: { val: 800, col: '#000000' },
        צ: { val: 90, col: '#000000' },
        ץ: { val: 900, col: '#000000' },
        ק: { val: 100, col: '#000000' },
        ר: { val: 200, col: '#000000' },
        שׁ: { val: 300, col: '#000000' },
        שׂ: { val: 300, col: '#000000' },
        תּ: { val: 400, col: '#000000' },
        ת: { val: 400, col: '#000000' }
      }
    }
  },
  computed: {
    navigation() {
      return Object.keys(this.bibleObj.Torah)
    }
  },
  methods: {
    toHeb(x) {
      return this.map[x] ? this.map[x] : x
    },
    editVerse(e, index) {
      e.preventDefault()
      this.customize[index].edit = !this.customize[index].edit
    },
    applyValue(e, index) {
      e.preventDefault()
      let verseStyle = this.$refs.verse[index].innerHTML
      const simpleVerse = verseStyle.replace(/[\u0591-\u05C7 \s]/g, '')
      let wordSum = 0
      let sentenceSum = 0
      for (let i = 2; i < simpleVerse.length; i++) {
        const letter = simpleVerse.charAt(i)
        if (letter in this.hebLetterMap) {
          wordSum += this.hebLetterMap[letter].val
          if (simpleVerse.charCodeAt(i) === 1488) {
            sentenceSum += wordSum
            wordSum = 0
          }
        }
      }
      for (const i in this.hebLetterMap) {
        const re = new RegExp(i, 'g')
        verseStyle = verseStyle.replace(
          re,
          i + '<sub>' + this.hebLetterMap[i].val + '  </sub>'
        )
      }
      verseStyle += '<sup>' + sentenceSum + '  </sup>'
      this.$refs.verse[index].innerHTML = verseStyle
    },
    applyColor(e, index) {
      e.preventDefault()
      let verseStyle = this.$refs.verse[index].innerHTML
      for (const i in this.hebLetterMap) {
        const letter = this.hebLetterMap[i].letter
        const re = new RegExp(letter, 'g')
        verseStyle = verseStyle.replace(
          re,
          '<span style="color:' +
            this.hebLetterMap[i].col +
            '">' +
            letter +
            '</span>'
        )
      }
      this.$refs.verse[index].innerHTML = verseStyle
    },
    showCustomizeOption(e, index) {
      e.preventDefault()
      this.customize[index].icon = !this.customize[index].icon
    },
    hideCustomizeOption(e, index) {
      e.preventDefault()
      this.customize[index].icon = !this.customize[index].icon
    }
  }
}
</script>
<style>
.heb {
  font-family: 'David Libre', serif;
  text-align: right;
}

.heb span {
  font-size: larger;
}

li {
  list-style-type: none;
}

table {
  table-layout: fixed;
  width: 100%;
}
td {
  width: 25%;
}
sup {
  font-size: 8px;
  color: hsl(240, 96%, 82%);
}
sub {
  font-size: 6px;
  color: grey;
  left: 0.75em;
  top: 2.25em;
  -webkit-writing-mode: vertical-lr;
  -ms-writing-mode: tb-lr;
  writing-mode: vertical-lr;
}
i {
  display: block;
  cursor: pointer;
  font-size: small;
}
</style>
