<template>
  <div class="StyleEditor">
    <form @submit.prevent="save" class="StyleEditor-form">
      <label for="var-brand-primary">
        Brand Primary
      </label>
      <input
        type="text"
        class="StyleEditor-input"
        v-model="input"
        @input="$emit('input', $event.target.value);"
      >
      <input type="submit">
    </form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      input: '',
    };
  },
  methods: {
    save () {
      console.log('saving...')
    }
  }
}
</script>