<template>
  <div>
    <input
      :value="modelValue" 
      @input="$emit('update:modelValue', $event.target.value)"
      :placeholder="placeholder"
      @keyup.enter="onEnter"
      type="text"
    />
    <!-- <i class="ri-send-plane-2-fill" @click="onEnter"></i> -->
  </div>
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    modelValue: String,
    placeholder: {
      type: String,
      default: 'Enter text',
    },
  },
  emits: ['update:modelValue', 'enter'],
  methods: {
    onEnter() {
      this.$emit('enter');
    },
  },
};
</script>
