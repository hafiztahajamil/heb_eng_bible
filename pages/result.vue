<template>
  <b-container>
    <b-row>
      <navbar />
      <b-col col xs="6" md="8" xl="9">
        <b-row align-h="end">
          <n-checkbox v-model="lang.eng">Eng</n-checkbox>
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
            >
            </i>
          </n-button>
        </b-row>
        <b-row>
          <b-col>
            <h3 v-if="lang.heb" class="heb">בְּרֵאשִׁית</h3>
          </b-col>
          <b-col>
            <h3 v-if="lang.eng">Genesis</h3>
          </b-col>
        </b-row>
        <table class="table">
          <thead>
            <tr>
              <th>
                <h5 v-if="lang.heb" class="heb">1 פרק</h5>
              </th>
              <th>
                <h5 v-if="lang.eng">Chapter 1</h5>
              </th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(verse, index) in bibleObj.Torah.Genesis[0]"
              :key="index"
            >
              <td
                class="heb"
                @mouseenter="showCustomizeOption($event, index)"
                @mouseleave="hideCustomizeOption($event, index)"
              >
                <span v-show="customize[index].icon && !customize[index].edit">
                  <i
                    v-b-tooltip.hover
                    title="Edit Verse"
                    class="far fa-lg fa-edit"
                    @click="editVerse($event, index)"
                  ></i>
                  <i
                    v-b-tooltip.hover
                    title="Apply Color"
                    class="fas fa-lg fa-fill-drip"
                    @click="applyColor($event, index)"
                  ></i>
                  <i
                    v-b-tooltip.hover
                    title="Show Value"
                    class="fas fa-lg fa-info"
                    @click="applyValue($event, index)"
                  ></i>
                </span>
                <span v-if="lang.heb && !customize[index].edit" ref="verse">{{
                  toHeb(index + 1) + '.' + verse.he
                }}</span>
                <b-textarea
                  v-if="lang.heb && customize[index].edit"
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
              <td>
                <span v-if="lang.eng">{{ index + 1 + '. ' + verse.eng }}</span>
              </td>
            </tr>
          </tbody>
        </table>
      </b-col>
    </b-row>
    <modal :show.sync="modals.palette" header-classes="justify-content-center">
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
          <n-button
            type="success-outline"
            @click="modals.palette = !modals.palette"
          >
            Save
          </n-button>
          <n-button type="danger" @click="modals.palette = !modals.palette">
            Close
          </n-button>
        </span>
      </b-container>
    </modal>
  </b-container>
</template>
<script>
import Swatches from 'vue-swatches'
import 'vue-swatches/dist/vue-swatches.min.css'
import navbar from './components/navbar'
import { Checkbox, FormGroupInput, Button, Modal } from '@/components'
import demoBible from '@/assets/bible.json'
export default {
  layout: 'reading',
  name: 'Result',
  components: {
    navbar,
    [Button.name]: Button,
    [Checkbox.name]: Checkbox,
    [FormGroupInput.name]: FormGroupInput,
    Modal,
    Swatches
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
      customize: [
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
        '0': '-',
        '1': 'א',
        '2': 'ב',
        '3': 'ג',
        '4': 'ד',
        '5': 'ה',
        '6': 'ו',
        '7': 'ז',
        '8': 'ח',
        '9': 'ט',
        '10': 'י'
      },
      hebLetterMap: [
        { letter: 'א', val: 1, col: '#000000' },
        { letter: 'בּ', val: 2, col: '#000000' },
        { letter: 'ב', val: 2, col: '#000000' },
        { letter: 'ג', val: 3, col: '#000000' },
        { letter: 'ד', val: 4, col: '#000000' },
        { letter: 'ה', val: 5, col: '#000000' },
        { letter: 'ו', val: 6, col: '#000000' },
        { letter: 'ז', val: 7, col: '#000000' },
        { letter: 'ח', val: 8, col: '#000000' },
        { letter: 'ט', val: 9, col: '#000000' },
        { letter: 'י', val: 10, col: '#000000' },
        { letter: 'כּ', val: 20, col: '#000000' },
        { letter: 'כ', val: 20, col: '#000000' },
        { letter: 'ךּ', val: 30, col: '#000000' },
        { letter: 'ך', val: 30, col: '#000000' },
        { letter: 'ל', val: 30, col: '#000000' },
        { letter: 'מ', val: 40, col: '#000000' },
        { letter: 'ם', val: 600, col: '#000000' },
        { letter: 'נ', val: 50, col: '#000000' },
        { letter: 'ן', val: 500, col: '#000000' },
        { letter: 'ס', val: 60, col: '#000000' },
        { letter: 'ע', val: 70, col: '#000000' },
        { letter: 'פּ', val: 80, col: '#000000' },
        { letter: 'ף', val: 800, col: '#000000' },
        { letter: 'צ', val: 90, col: '#000000' },
        { letter: 'ץ', val: 900, col: '#000000' },
        { letter: 'ק', val: 100, col: '#000000' },
        { letter: 'ר', val: 200, col: '#000000' },
        { letter: 'שׁ', val: 300, col: '#000000' },
        { letter: 'שׂ', val: 300, col: '#000000' },
        { letter: 'תּ', val: 400, col: '#000000' },
        { letter: 'ת', val: 400, col: '#000000' }
      ]
    }
  },
  computed: {
    sliceArray(index) {
      const start = index * 10 - index
      const end = (index - 1) * (index + 10)
      return this.hebLetterMap.slice(start, end)
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
      for (const i in this.hebLetterMap) {
        const letter = this.hebLetterMap[i].letter
        const re = new RegExp(letter, 'g')
        verseStyle = verseStyle.replace(
          re,
          letter + '<sup>' + this.hebLetterMap[i].val + '  </sup>'
        )
      }
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
  font-family: 'Frank Ruhl Libre', serif;
  text-align: right;
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
  color: blue;
}
i {
  display: block;
  cursor: pointer;
}
</style>
