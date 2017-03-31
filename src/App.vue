<template>
  <div class="text-center" id="app">
    <h1>Word Translator</h1>
    <h5 class="text-muted">Powered By Vue.js</h5>
    <hr>
    <TranslateForm v-on:formSubmit="translateText"></TranslateForm>
    <TranslateOutput v-text="translatedText"></TranslateOutput>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput';

export default {
  name: 'app',
  components:{
    TranslateForm,
    TranslateOutput
  },
  data: function(){
    return {
      translatedText:''
    }
  },
  methods: {
    translateText:function(text, language){
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20170329T180255Z.3c18d2dc7b65d525.f23ed9a9efa992bded4ef96334e3c154f61d2dea&lang='+language+'&text='+text)
      .then((response) => {
        this.translatedText = response.body.text[0];
      });
    }
  }
}
</script>

<style>
body {
  background:#fefefe;
}
</style>
