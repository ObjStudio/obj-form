<!--
 * @Author: 陈伟亮 1186723967@qq.com
 * @Date: 2022-07-07 18:22:29
 * @LastEditors: chenkangxu
 * @LastEditTime: 2022-07-22 20:24:39
 * @FilePath: \objectStudio\obj-form\packages\obj-modal.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template >
  <div>
    <el-dialog
      v-drag="enableDrag"
      :close-on-click-modal="false"
      v-bind="modalConfig"
      v-on="modalEvent"
      :visible.sync="modalConfig.show"
    >
      <div class="el-dialog-div" :style="{ height }">
        <slot name="dialog__content">
          <slot name="dialog__before"></slot>
          <obj-form
            ref="objForm"
            :formData="modalData"
            :formCols="modalCols"
            :formConfig="modalConfig"
          />
          <slot name="dialog__after"></slot>
        </slot>
      </div>

      <span slot="footer" class="dialog-footer">
        <el-button
          v-for="item in modalHandles"
          :key="item.prop"
          v-bind="item"
          v-on="item.event"
          :disabled="item.disabled && item.disabled(modalData[item.prop])"
          @click="
            item.submit
              ? $refs.objForm.globalVerify(item.handle)
              : item.handle()
          "
          >{{ item.label }}</el-button
        >
      </span>
    </el-dialog>
  </div>
</template>
<script>
import objForm from "./obj-form.vue";
import directives from "./js/directives.js";
export default {
  directives:directives,
  components: { objForm },
  props: {
    height: {
      type: String,
      default: null,
    },
    modalConfig: {
      type: Object,
      default: () => {},
    },
    modalCols: {
      type: Array,
      default: () => [],
    },
    modalData: {
      type: Object,
      default: () => {},
    },
    modalEvent: {
      type: Object,
      default: () => {},
    },
    modalHandles: {
      type: Array,
      default: () => [],
    },
    /**
     * 是否可推拽
     */
    enableDrag: {
      type: Boolean,
      default: true,
    },
  },
};
</script>
<style >
</style>