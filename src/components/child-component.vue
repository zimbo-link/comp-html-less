<template>
    <div style="margin: 10px;">
        <div>
            <h3>HTML</h3>
            <p>
                <textarea 
                    v-model="markup" ref="html"
                    @change="updateHtml($event.target.value)" 
                    rows="10" cols="140">
                </textarea>
            </p>
        </div>
        <div>
            <h3>LESS</h3>
            <p>
                <textarea 
                    v-model="lessc" ref="less"
                    @change="updateHtml($event.target.value)" 
                    rows="10" cols="140">
                </textarea>
            </p>
        </div>
    </div>
</template>
<script setup>
/* eslint-disable */
import { ref, defineEmits, onMounted } from 'vue';
import {LessElement} from "../assets/js/LessElement.js";

require('../assets/js/less.min.js');

if(customElements.get('less-render') === undefined){
    customElements.define('less-render', LessElement);
}

const emit = defineEmits(['change-html'])

const markup = ref(`<div style="background-color:#fff;margin:40px; padding: 20px">
<h3>Get in touch! (blue indicates scoped style)</h3>
<hr>
<h4>Francessca McNulty</h4>
<p>International Officer (Europe & Latin America) Student Recruitment and Bussiness Development</p>
<a href="#" style="display:block;text-align:right;">>></a>
</div>`)

const lessc = ref(`@width: 100%;
@height: 1.5em;
@mainColor: #3366ff;
@secondColor: #0099ff;

h3 {
  width: @width;
  height: @height;
  font-size: 24px;
  line-height: 2em;
  color: @mainColor;
}
h4 {
  width: @width;
  height: @height;
  font-size: 18px;
  line-height: 1.5em;
  color: @secondColor;
}`)

const updateHtml = () => {
    less.render(lessc.value) 
    .then(output => {
        let tmpl = `
            <style type="text/css">${output.css}</style> 
            ${markup.value}
        `; 
        emit('change-html', tmpl);
    },
    function(error) {
        alert(error.message);
    });
}
 
onMounted(() => {
    updateHtml();
})

</script>