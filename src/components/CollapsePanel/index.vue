<template>
  <div
    class="overflow-hidden transition-all duration-150"
    :style="{ height: height + 'px' }"
  >
    <div ref="main">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    visible: {
      type: Boolean,
      default: false
    },
    baseHeight: {
      type: Number,
      default: 40
    }
  },

  data() {
    return {
      height: this.baseHeight
    }
  },

  watch: {
    visible(val) {
      val ? this.open() : this.close()
    }
  },

  mounted() {
    if (this.visible) {
      this.open()
    }

    window.addEventListener('resize', this.onResize)
    this.$once('hook:beforeDestroy', () => {
      window.removeEventListener('resize', this.onResize)
    })
  },

  methods: {
    open() {
      this.height = this.$refs.main.clientHeight
    },

    close() {
      this.height = this.baseHeight
    },

    onResize() {
      clearTimeout(this._timer)
      this._timer = setTimeout(() => {
        if (this.visible) {
          this.open()
        }
      }, 60)
    }
  }
}
</script>

<style lang="scss" scoped></style>
