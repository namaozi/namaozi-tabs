<template>
  <div>
    <Score :song="this.song" />
    <HorizontalTab :score-array="scoreArray" :beats="this.song['beats']" :capo="this.song['capo']"
                   :position="this.song['position']" :tuning="this.song['tuning']" />
    <VerticalTab :score-array="scoreArray" />
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
    data: function () {
      return {
        scoreArray: this.parse(this.song.score),
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
              if (fragment.match(/^[1-6]/) !== null) {
                const key = fragment[0];
                const value = fragment.slice(1);
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
