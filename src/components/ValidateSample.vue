<template>
  <div class="wrapper">
    <validation-observer ref="validationObserver" tag="div">
      <h1>さんすう　テスト①</h1>
      <div class="name-box">
        <div class="col-3"><p class="margin-0">なまえ：</p></div>
        <div class="col-9">
          <validation-provider rules="required" v-slot="{ errors }">
            <input type="text" v-model="name" name="name">
            <div v-if="errors[0]" class="error">{{ errors[0] }}</div>
          </validation-provider>
          </div>
      </div>
      <h2 class="align-left margin-top-3rem">1.&nbsp;&nbsp;&nbsp;けいさんをしましょう</h2>
      <ol class="question-list">
        <li v-for="(qa, index) in qas" v-bind:key="index" class="qa">
          <div class="col-1">( {{ index + 1 }} )</div>
          <div class="col-8">{{ qa.question }}</div>
          <div class="col-1">=</div>
          <div class="col-2">
            <validation-provider rules="required" v-slot="{ errors }">
              <input type="text" v-model="qa.answer" name="answer">
              <div v-if="errors[0]" class="error">{{ errors[0] }}</div>
            </validation-provider>
          </div>
        </li>
      </ol>
    </validation-observer>
    <button type="button" v-on:click="errCheck">こたえあわせ！</button>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import { ValidationProvider, ValidationObserver, extend } from 'vee-validate';
import { required } from 'vee-validate/dist/rules';
import { ElForm } from 'element-ui/types/form';

extend('required', {
  ...required,
  message: 'きにゅうしてね',
});

@Component({
  components: {
    ValidationProvider,
    ValidationObserver,
  },
})
export default class ValidateSample extends Vue {

  public $refs!: { [key: string]: ElForm };

  private name: string = '';
  private qas: any[] = [
    { question: '９＋５－９', answer: '' },
    { question: '６＋８－４', answer: '' },
    { question: '８＋４－９', answer: '' },
    { question: '７＋９－５', answer: '' },
    { question: '１０＋２－１０', answer: '' },
    { question: '８＋９－９', answer: '' },
    { question: '３＋７－９', answer: '' },
    { question: '６＋７－７', answer: '' },
    { question: '７＋８－６', answer: '' },
    { question: '１＋８－７', answer: '' },
  ];

  public async errCheck() {
    this.$refs.validationObserver.validate();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapper {
  max-width: 1080px;
  margin: auto;
}

.name-box {
  display: flex;
  font-size: 2rem;
}

input {
  padding: 0.5rem 0;
  font-size: 2rem;
  width: 100%;
  border-top: solid 0px transparent;
  border-left: solid 0px transparent;
  border-right: solid 0px transparent;
}

input:focus {
  outline-style: none;
  border-bottom: solid 2px skyblue;
}

.question-list {
  width: 100%;
  margin: 0;
  padding: 0;
  padding-left: 1rem;
  font-size: 1.5rem;
}

.qa {
  display: flex;
  padding: 1rem 0;
  text-align: left;
}

.qa div {
  margin: auto 0;
}

.error {
  color: red;
}

.align-left {
  text-align: left;
}

.margin-0 {
  margin: 0;
}

.margin-top-3rem {
  margin-top: 3rem;
}

.col-1 {
  width: 8.3333%;
}

.col-2 {
  width: 16.6666%;
}

.col-3 {
  width: 25%;
}

.col-6 {
  width: 50%;
}

.col-8 {
  width: 66.6666%;
}
.col-9 {
  width: 75%;
}
</style>
