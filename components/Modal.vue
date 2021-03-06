<template>
  <SlideYUpTransition :duration="animationDuration">
    <div
      v-show="show"
      class="modal fade"
      :class="[
        { 'show d-block': show },
        { 'd-none': !show },
        { 'modal-mini': type === 'mini' }
      ]"
      tabindex="-1"
      role="dialog"
      :aria-hidden="!show"
      @click.self="closeModal"
    >
      <div
        class="modal-dialog"
        :class="[{ 'modal-notice': type === 'notice' }, modalClasses]"
      >
        <div class="modal-content">
          <slot name="base-content">
            <div class="modal-header" :class="headerClasses">
              <slot name="close-button">
                <button
                  v-if="showClose"
                  type="button"
                  class="close"
                  data-dismiss="modal"
                  :aria-hidden="!show"
                  @click="closeModal"
                >
                  <i class="now-ui-icons ui-1_simple-remove"></i>
                </button>
              </slot>
              <slot name="header"></slot>
            </div>

            <div class="modal-body" :class="bodyClasses">
              <slot></slot>
            </div>

            <div class="modal-footer" :class="footerClasses">
              <slot name="footer"></slot>
            </div>
          </slot>
        </div>
      </div>
    </div>
  </SlideYUpTransition>
</template>
<script>
import { SlideYUpTransition } from 'vue2-transitions'

export default {
  name: 'Modal',
  components: {
    SlideYUpTransition
  },
  props: {
    show: Boolean,
    showClose: {
      type: Boolean,
      default: true
    },
    type: {
      type: String,
      default: '',
      validator(value) {
        const acceptedValues = ['', 'notice', 'mini']
        return acceptedValues.includes(value)
      }
    },
    modalClasses: [Object, String],
    headerClasses: [Object, String],
    bodyClasses: [Object, String],
    footerClasses: [Object, String],
    animationDuration: {
      type: Number,
      default: 500
    }
  },
  watch: {
    show(val) {
      const documentClasses = document.body.classList
      if (val) {
        documentClasses.add('modal-open')
      } else {
        documentClasses.remove('modal-open')
      }
    }
  },
  methods: {
    closeModal() {
      this.$emit('update:show', false)
      this.$emit('close')
    }
  }
}
</script>
<style>
.modal.show {
  background-color: rgba(0, 0, 0, 0.3);
}
</style>
