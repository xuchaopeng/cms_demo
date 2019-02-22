<template>
  <el-input-number v-model="numbers" @change="handleChange" :min="1" :max="10" label="描述文字"></el-input-number>
</template>
<script>
export default {
  props: {
    min: {
      default: 1,
      type: Number
    },
    max: {
      default: 10,
      type: Number
    }
  },
  data() {
    return {
      numbers: 1
    }
  },
  created() {},
  methods: {
    handleChange(value) {
      this.$emit('numberChange', value)
    }
  }
}
</script>
