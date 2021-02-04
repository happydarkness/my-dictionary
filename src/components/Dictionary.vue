<template>
  <div class="dictionary">
    <div class="options">
      <p class="dictionary-length-info">Your dictionary - {{ words.length }}</p>
      <div class="option-buttons">
        <button class="option-button add-button">Add new word</button>
        <button class="option-button delete-button">Delete word</button>
      </div>
    </div>
    <div class="filters">
      <p class="filter-text">Filters:</p>
      <label for="alphabet" class="filter-label" >In alphabet order</label>
      <input type="radio" class="filter-radio" id="alphabet" name="filter" value="alphabet">
      <label for="random" class="filter-label">In random order</label>
      <input type="radio" class="filter-radio" id="random" name="filter" value="random"> 
      <label for="time" class="filter-label">In order of time</label>
      <input type="radio" class="filter-radio" id="time" name="filter" value="time">
    </div>
    <div class="dictionary-main">
      <div class="word" v-for="word of currentWords" :key="word.key">
        <p class="word-text">{{ word.word + ' - ' + word.translate }}</p>
        <div class="word-audio"><img src="./../../public/img/volume.png" alt="" class="audio-img" @click="playAudio($event,word.word)"><audio></audio></div>
      </div>
    </div>
    <div class="change-page">
      <div class="left-arrow"></div>
      <div class="nums">
        <router-link v-if="previousPage > firstPage" :to="{name: 'Dictionary', params: { pageId: firstPage }}"> {{ firstPage }} </router-link>
        <p v-if="previousPage - 1 > firstPage" class="dots-link"> ... </p>
        <router-link class="page-link" v-if="previousPage > 0" :to="{name: 'Dictionary', params: { pageId: previousPage }}" > {{ previousPage }} </router-link>
        <router-link class="page-link" :to="{name: 'Dictionary', params: { pageId: currentPage }}"> {{ currentPage }} </router-link>
        <router-link class="page-link" v-if="nextPage <= lastPage" :to="{name: 'Dictionary', params: { pageId: nextPage }}"> {{ nextPage }}</router-link>
        <p v-if="nextPage + 1 < lastPage" class="dots-link"> ... </p>
        <router-link class="page-link" v-if="nextPage < lastPage" :to="{name: 'Dictionary', params: { pageId: lastPage }}" > {{ lastPage }}</router-link>
      </div>
      <div class="right-arrow"></div>
    </div>
  </div>
  <new-word v-if="newWordVision"></new-word>
</template>

<script>
import NewWord from './NewWord.vue'


// ошибка выскакивает из-за добавления NewWord
export default {
  components:{
    'new-word': NewWord,
  },
  name: "Dictionary",
  data() {
    return {
      firstPage: 1,
      rer: 0,
      wordsOnPage: 10,
      newWordVision: false,
      words: [
        {word:'make dinner', translate: ['делать завтрак'],key:1},
        {word:'word', translate: ['слово'],key:2},
        {word:'friendly', translate: ['дружелюбный'],key:3},
        {word:'volume', translate: ['объем', 'громкость'],key:4},
        {word:'ability', translate: ['способность'],key:5},
        {word:'abbreviation', translate: ['аббревиатура'],key:6},
        {word:'bdfdfbdf', translate: ['аббревиатура'],key:7},
        {word:'bdfbfd', translate: ['аббревиатура'],key:8},
        {word:'lo;lgv', translate: ['аббревиатура'],key:9},
        {word:'b,jtbfk.kjg.jk', translate: ['аббревиатура'],key:10},
        {word:'Bo', translate: ['делать завтрак'],key:11},
        {word:'word', translate: ['слово'],key:12},
        {word:'friendly', translate: ['дружелюбный'],key:13},
        {word:'volume', translate: ['объем', 'громкость'],key:14},
        {word:'ability', translate: ['способность'],key:15},
        {word:'abbreviation', translate: ['аббревиатура'],key:16},
        {word:'bdfdfbdf', translate: ['аббревиатура'],key:17},
        {word:'bdfbfd', translate: ['аббревиатура'],key:18},
        {word:'lo;lgv', translate: ['аббревиатура'],key:19},
        {word:'b,jtbfk.kjg.jk', translate: ['аббревиатура'],key:20},
        {word:'RE', translate: ['делать завтрак'],key:21},
        {word:'word', translate: ['слово'],key:22},
        {word:'friendly', translate: ['дружелюбный'],key:23},
        {word:'volume', translate: ['объем', 'громкость'],key:24},
        {word:'ability', translate: ['способность'],key:25},
        {word:'abbreviation', translate: ['аббревиатура'],key:26},
        {word:'bdfdfbdf', translate: ['аббревиатура'],key:27},
        {word:'bdfbfd', translate: ['аббревиатура'],key:28},
        {word:'lo;lgv', translate: ['аббревиатура'],key:29},
        {word:'b,jtbfk.kjg.jk', translate: ['аббревиатура'],key:30},
        {word:'SE', translate: ['делать завтрак'],key:31},
        {word:'word', translate: ['слово'],key:32},
        {word:'friendly', translate: ['дружелюбный'],key:33},
        {word:'volume', translate: ['объем', 'громкость'],key:34},
        {word:'ability', translate: ['способность'],key:35},
        {word:'abbreviation', translate: ['аббревиатура'],key:36},
        {word:'bdfdfbdf', translate: ['аббревиатура'],key:37},
        {word:'bdfbfd', translate: ['аббревиатура'],key:38},
        {word:'lo;lgv', translate: ['аббревиатура'],key:39},
        {word:'b,jtbfk.kjg.jk', translate: ['аббревиатура'],key:40},
        {word:'23r', translate: ['делать завтрак'],key:41},
        {word:'word', translate: ['слово'],key:42},
        {word:'friendly', translate: ['дружелюбный'],key:43},
        {word:'volume', translate: ['объем', 'громкость'],key:44},
        {word:'ability', translate: ['способность'],key:45},
        {word:'abbreviation', translate: ['аббревиатура'],key:46},
        {word:'bdfdfbdf', translate: ['аббревиатура'],key:47},
        {word:'bdfbfd', translate: ['аббревиатура'],key:48},
        {word:'lo;lgv', translate: ['аббревиатура'],key:49},
        {word:'b,jtbfk.kjg.jk', translate: ['аббревиатура'],key:50},
      ]
    }
  },
  methods: {
    playAudio($event, word) {
      let audio =  $event.target.closest('.word-audio').querySelector('audio');
      audio.src = `http://api.voicerss.org/?key=223d72c515914b83827fa3845b182ba5&hl=en-us&v=John&f=24khz_16bit_stereo&src=${encodeURI(word)}`;
      audio.play();
    },
    pageChange(value) {
      this.currentPage = value;
    }
  },
  computed: {
    currentPage() {
      if (this.$route.params.pageId) {
        return +this.$route.params.pageId;
      }
      return 1;
    },
    previousPage() {
      return this.currentPage - 1;
    },
    nextPage() {
      return this.currentPage + 1;
    },
    lastPage() {
      return Math.ceil(this.words.length / this.wordsOnPage);
    },
    currentWords() {
      if (this.currentPage >= this.firstPage && this.currentPage <= this.lastPage) {

        let minNum = (this.currentPage - 1) * this.wordsOnPage;
        if (this.words - minNum < 10) {
          return this.words.slice(minNum, this.words);
        } else {
          return this.words.slice(minNum, minNum + this.wordsOnPage);
        }

      }

      return '';
    },
  }
}
</script>

<style lang="sass" scoped>
.dictionary
  height: 1100px
  background: $light-theme-color
  box-shadow: 0 0 4px rgba(0 , 0 , 0, 0.25)
  margin-right: 6%
  margin-top: 28px
  .options
    display: flex
    justify-content: space-between
    align-items: baseline
    padding: 25px 35px 25px 60px
    height: 100px
    width: 100%
    .dictionary-length-info
      font-size: 20px
      color: $main-dark-text-color
      flex: 1
    .option-buttons
      display: flex
      flex: 1
      justify-content: flex-end
      .option-button
        width: 160px
        height: 46px
        font-size: 18px
        border: 0
        background: $main-dictionary-button-color
        margin-left: 25px
        color: $main-dark-text-color
  .filters
    height: 95px
    background: #DFF9FB
    display: flex
    align-items: center
    justify-content: space-between
    padding-left: 31px
    padding-right: 54px
    color: $main-dark-text-color
    .filter-text
      font-size: 20px
      margin-bottom: 10px
    .filter-radio
      font-size: 18px
      appearance: none
      width: 30px
      height: 30px
      position: relative
      top: -2px
      background: $light-theme-color
      outline: none
      &:before
        content: ''
        display: block
        background-size: contain
        width: 100%
        height: 100%
        outline: none !important
        transition: 0.2s
        opacity: 0
      &:checked
        &:before
          background: url("./../../public/img/check-mark.png") no-repeat
          background-size: contain
          opacity: 1
  .dictionary-main
    width: 100%
    display: flex
    flex-wrap: wrap
    .word
      flex:1  calc(50% - 2*12px)
      height: 140px
      background: $main-dictionary-word-bg
      margin: 12px
      display: flex
      justify-content: space-between
      align-items: center
      font-size: 20px
      padding-left: 30px
      padding-right: 20px
      .word-audio
        width: 32px
        height: 32px
        display: flex
        justify-content: center
        margin-top: -10px
  .change-page
    .nums
      display: flex
      justify-content: center
      align-items: center
      padding-top: 10px
      .page-link
        font-size: 20px
        text-decoration: none
        &.router-link-active
          color: $main-dark-text-color
          position: relative
          &:after
            content: ""
            background: $main-dark-text-color
            width: 12px
            height: 2px
            position: absolute
            bottom: 8px
            left: calc(50% - 6px)
      > a,p
        padding: 7px
      .dots-link
        font-size: 20px
        margin: 0px
</style>