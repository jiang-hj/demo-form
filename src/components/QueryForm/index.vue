<template>
  <div>
    <collapse-panel :visible="isOpen">
      <el-form
        ref="form"
        :model="form"
        label-width="80px"
        :inline="false"
        size="normal"
      >
        <div class="grid grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
          <div v-for="(item, i) in fields" :key="i" class="col">
            <el-form-item
              :label="item.label"
              size="normal"
              :prop="item.name"
              :rules="item.rules || []"
            >
              <!-- {{ i }} -->
              <component
                :is="item.tag"
                v-model="form[item.name]"
                :placeholder="item.placeholder"
                v-bind="item.props || {}"
                :options="item.options || []"
                style="width: 210px"
              >
                <template
                  v-if="item.tag === 'el-select' && Array.isArray(item.options)"
                >
                  <el-option
                    v-for="(op, j) in item.options"
                    :key="j"
                    :label="op.label"
                    :value="op.value"
                  />
                </template>
                <template v-for="(slot, k) in item.__slot__">
                  <span
                    v-if="['number', 'string'].includes(typeof slot)"
                    :key="k"
                    :slot="k"
                  >{{ slot }}</span>
                  <template v-if="!item.options && Array.isArray(slot)">
                    <el-option
                      v-for="(op, j) in slot"
                      :key="j"
                      :label="op.label"
                      :value="op.value"
                    />
                  </template>
                </template>
              </component>
            </el-form-item>
          </div>
          <div
            class="col-start-2 col-end-3 row-start-1 lg:(col-start-3 col-end-4) xl:(col-start-4 col-end-5)"
          >
            <el-form-item label-width="0" size="normal">
              <el-button
                type="primary"
                size="mini"
                class="mr-1"
                @click="queryHandle"
              >查询</el-button>
              <el-button
                type="primary"
                size="mini"
                class="mr-1"
                @click="reset"
              >重置</el-button>

              <span class="inline-block w-24 text-right">
                <el-button
                  type="text"
                  size="small"
                  class="text-sm"
                  :class="[
                    {
                      invisible: fields.length < 2,
                      'lg:invisible': fields.length < 3,
                      'xl:invisible': fields.length < 4
                    }
                  ]"
                  @click="isOpen = !isOpen"
                >{{ isOpen ? '收起' : '展开更多' }}
                  <i
                    class="el-icon-d-arrow-right transform transition"
                    :class="[isOpen ? '-rotate-90' : 'rotate-90']"
                  />
                </el-button>
              </span>
            </el-form-item>
          </div>
        </div>
      </el-form>
    </collapse-panel>
  </div>
</template>

<script>
import CollapsePanel from '@/components/CollapsePanel'

export default {
  components: {
    CollapsePanel
  },

  props: {
    fields: {
      type: Array,
      default: null
    }
  },

  data() {
    return {
      isOpen: false,
      form: {}
    }
  },

  watch: {
    fields() {
      this.form = {}
    }
  },

  methods: {
    queryHandle() {
      this.$notify.success(JSON.stringify(this.form))
    },
    reset() {
      this.$refs.form.resetFields()
    }
  }
}
</script>

<style lang="scss" scoped></style>
