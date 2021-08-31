<template>
  <transition name="el-loading-fade" @after-leave="handleAfterLeave">
    <div
      v-show="visible"
      class="el-loading-mask"
      :style="{ backgroundColor: background || '' }"
      :class="[customClass, { 'is-fullscreen': fullscreen }]">
      <div class="el-loading-spinner">
        <svg v-if="!spinner" class="circular" viewBox="25 25 50 50">
          <circle class="path" cx="50" cy="50" r="20" fill="none"/>
        </svg>
        <i v-else :class="spinner"></i>
				<p v-if="text" class="el-loading-text">{{ text }}<span v-show="isNumber">{{percent}}%</span></p>
      </div>
      <i class="el-icon-close el-loading-close" @click="hideLoading" v-show="customClose"></i>
    </div>
  </transition>
</template>

<script>
  export default {
    data() {
      return {
        text: null,
        spinner: null,
        background: null,
        fullscreen: true,
        visible: false,
        hiding: false,
        customClass: false,
        customClose: false,
        percent: ''
      };
    },

    methods: {
      handleAfterLeave() {
        this.$emit('after-leave');
      },
      setText(text) {
        this.text = text;
      },
      hideLoading() {
        this.visible = false;
        this.hiding = true;
      },
      isNumber() {
        return (typeof this.percent) === 'number';
      }
    }
  };
</script>
