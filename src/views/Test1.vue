<template>
  <b-container>
    <b-row>
      <b-col cols="12">
        <div class="question-container d-flex mb-4">
          <label
            for="question"
            class="question-container__items-title items-title mr-3"
            >Вопрос:</label
          >
          <b-form-input
            id="question"
            :state="questionState"
            class="question-container__input input"
            v-model="sharePoint.question"
          ></b-form-input>
        </div>
      </b-col>
      <!-- answer type -->
      <b-col cols="12">
        <div class="answer-type-container d-flex mb-4">
          <label
            for="answerType"
            class="question-container__items-title items-title mr-3"
            >Тип ответа:</label
          >
          <b-form-select
            id="answerType"
            class="answer-type-container__select select"
            v-model="typeAnswer"
            :options="options.typeAnswer"
          ></b-form-select>
        </div>
      </b-col>
    </b-row>
    <b-row v-if="sharePoint.question.length > 2">
      <b-col cols="12" class="mb-4">
        <b-row>
          <b-col cols="8" class="items-title">Ответы:</b-col>
          <b-col cols="2" class="text-muted d-flex justify-content-center"
            >Верный</b-col
          >
          <b-col cols="2"></b-col>
        </b-row>
      </b-col>
      <b-col cols="12" class="answer-container">
        <b-row v-for="(item, i) in options.answers" :key="i" class="mb-3">
          <b-col cols="8" class="d-flex answer-container__item">
            <span class="answer-container__number">{{ i + 1 }})</span>
            <input class="form-control" v-model="item.value" type="text" />
          </b-col>
          <b-col cols="2" class="answer-container__item">
            <label class="radio" :for="`check${i}`">
              <input
                class="form-check-input"
                v-model="sharePoint.answers"
                :value="item.value"
                :type="typeAnswer"
                :id="`check${i}`"
              />
              <span></span>
            </label>
          </b-col>
          <b-col cols="2" class="answer-container__item">
            <button class="btn-action" @click="deleteAnswerField(i)">
              <b-icon icon="x-circle" variant="danger"></b-icon>
            </button>
          </b-col>
        </b-row>
      </b-col>
      <b-col cols="12" class="mt-3">
        <b-row>
          <b-col>
            <span class="answer-container__number"></span>
            <button class="btn-submit action" @click="addAnswerField">
              &#43;
            </button>
          </b-col>
        </b-row>
      </b-col>
      <b-col cols="12" class="d-flex justify-content-center mt-3">
        <button class="btn-submit" @click="complete">Готово</button>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  name: "Test1",
  data() {
    return {
      options: {
        typeAnswer: [
          { text: "Один верный", value: "radio" },
          { text: "Множественный выбор", value: "checkbox" },
        ],
        answers: [
          {
            value: "",
          },
        ],
      },
      typeAnswer: "radio",
      sharePoint: {
        question: "",
        typeAnswer: "",
        answers: [],
      },
    };
  },
  components: {},
  computed: {
    questionState() {
      return this.sharePoint.question.length > 2 ? true : false;
    },
  },
  methods: {
    complete(event) {
      event.preventDefault();
      this.sharePoint.typeAnswer = this.typeAnswer;
      console.log(this.sharePoint);
    },
    addAnswerField() {
      this.options.answers.push({
        value: "",
      });
    },
    deleteAnswerField(field) {
      this.options.answers.splice(field, 1);
    },
  },
  watch: {
    typeAnswer() {
      this.sharePoint.answers = [];
    },
  },
};
</script>
