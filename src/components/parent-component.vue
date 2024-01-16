<template>
    <h1>Canvas</h1>
    <less-render ref="canvas" />
    <div style="margin: 10px">
        <h1>Editor</h1>
        <child-component v-on:change-html="changeHtml" />
    </div>
</template>

<style lang="less">
    @bgColor: #f1f1f1;
    @notShadow: #000;
    #app {
        background: @bgColor;
        font-size: 100%;
    }
    h3 {
        color: @notShadow;
    }
</style>

<script setup>
import { ref } from 'vue';
import ChildComponent from "./child-component";

const canvas = ref(null);

const changeHtml = (tmpl) => {
    canvas.value.html(tmpl);
}
</script>
