<template>
  <div class="score-tab-container">
    <h1 class="is-size-1 has-text-weight-light has-text-centered">{{song['title']}}</h1>
    <div class="field is-horizontal">
      <div class="field-label is-normal">
        <label class="label">score:</label>
      </div>
      <div class="field-body">
        <div class="field">
          <div class="control">
            <textarea class="textarea" v-model="song['score']"></textarea>
          </div>
        </div>
      </div>
    </div>

    <HorizontalTab :score-array="scoreArray" :beats="song['beats']" :capo="song['capo']"
                   :position="song['position']" :tuning="song['tuning']" />
  </div>
</template>

<script>
  import Score from '../components/Score';
  import HorizontalTab from '../components/HorizontalTab';
  import VerticalTab from '../components/VerticalTab';

  export default {
    components: {
      Score,
      HorizontalTab,
      VerticalTab,
    },
    props: {
      song: {
        type: Object,
        required: true,
        default: 'song', // 降ってくるsong
      },
    },
    computed: {
      scoreArray: function () {
        return this.parse(this.song.score);
      }
    },
    methods: {
      /**
       * スコアをパースして表示させやすくオブジェクトにする
       * @param rawScore
       * @returns {{hoge: string}}
       */
      parse(rawScore) {
        const rawBars = rawScore.split('\n').map(raw => raw.slice(1, -1).split('|')).flat();
        const bars = rawBars.map((rawBar, index) => {
          let bar = {index: index + 1};
          const notes = rawBar.split(',')
            .map(fragment => {
              // 数字から始まる時,fragmentは単音
              // しかし 5X のような場合はミュート
              if (fragment.match(/^[1-6]/) !== null) {
                const key = fragment[0];
                const value = fragment.slice(1);
                if (value === "X") {
                  return;
                }
                return {[key]: value};
              }
              // [E,X,X,G,B,E] みたいなfragmentは6弦から書いた和音
              // {6: "E", 3: "G", 2: "B", 1: "E"} の形に変換する
              if (fragment[0] === '[' /*&& note.substr(note.length) === ']'*/) {
                const fragmentNotes = fragment.slice(1, -1).split(';');
                let chordComponents = {};
                fragmentNotes.forEach((note, i) => {
                  if (note !== 'x') {
                    return chordComponents[6 - i] = note;
                  }
                });
                return chordComponents;
              }
              // 空白は休符
              // {} 空オブジェクトにする
              return {};
            });
          bar['notes'] = notes;
          return bar;
        });
        return bars;
      }
    }
  }
</script>

<style scoped>
  .score-tab-container > * {
    margin: 10px 0;
  }
</style>
