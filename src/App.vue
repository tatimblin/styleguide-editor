<template>
  <div id="app" :style="cssProps">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <style-editor @input="test = $event" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import StyleEditor from './components/StyleEditor.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    StyleEditor,
  },
  data() {
    return {
      proxies: {
        headingLeadColor: 'brandPrimary',
        headingHeadColor: 'brandSecondary',
      },
      vars: {
        brandPrimary: 'red',
        brandSecondary: 'orange',
      },
      test: '',
    };
  },
  // TODO use vue-head to set a google font
  methods: {
    namingConventions(string, proxy) {
      const kebab = string
        .replace(/([a-z0-9])([A-Z])/g, '$1-$2')
        .replace(/([A-Z])([A-Z])(?=[a-z])/g, '$1-$2')
        .toLowerCase()

      return proxy ? `var(--${kebab})` : `--${kebab}`
    },
  },
  computed: {
    cssProps() {
      const customProperties = {};

      for (const property in this.vars) {
        const kebabKey = this.namingConventions(property)
        customProperties[kebabKey] = this.vars[property]
      }

      for (const property in this.proxies) {
        const kebabKey = this.namingConventions(property)
        const kebabValue = this.namingConventions(this.proxies[property], true)
        customProperties[kebabKey] = kebabValue
      }

      return customProperties;
    },
	},
}
</script>

<style-editor->
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style-editor->
