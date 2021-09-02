<template>
  <button @click="onClick()" v-bind:style="{background: color}" class="btn">{{btnText}}</button>
</template>

<script>
export default {
  name: "Button",
  props: {
    btnText: String,
    color: String,
  },
  methods: {
      onClick(){
          this.$emit('btn-click')
      }
  }
};
</script>

<style scoped>
.btn {
  display: flex;
  flex-direction: column;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
  
}
</style>