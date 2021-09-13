<template>
  <div>
    <input type="text" :placeholder="placeholder" v-model.trim="inputValue" />
    <button type="submit" @click="emitSearch">
      {{ buttonText || 'cerca' }}
    </button>
  </div>
</template>

<script>
export default {
  name: 'Search',
  data() {
    return {
      inputValue: '',
    };
  },
  props: ['placeholder', 'buttonText'],
  methods: {
    emitSearch() {
      this.$emit('search', this.inputValue);
      this.inputValue = '';
    },
  },
};
</script>

<style></style>
