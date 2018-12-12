<template>
  <div>
    {{/* 演奏情報 */}}
    <div class="horizontal-tab-controller">
      <div class="field is-horizontal">
        <div class="field-label is-normal">
          <label class="label">tuning:</label>
        </div>
        <div class="field-body">
          <div class="field">
            <div class="control">
              <input class="input is-normal" type="text" v-model="tuning">
            </div>
          </div>
        </div>
      </div>
      <div class="field is-horizontal">
        <div class="field-label is-normal">
          <label class="label">capo:</label>
        </div>
        <div class="field-body">
          <div class="field">
            <div class="control">
              <input class="input" type="number" v-model.number="capo">
            </div>
          </div>
        </div>
      </div>
      <div class="field is-horizontal">
        <div class="field-label is-normal">
          <label class="label">zoom:</label>
        </div>
        <div class="field-body">
          <div class="field">
            <div class="control">
              <input class="input-range is-primary" type="range" min="1"
                     :max="this.scoreArray.length"
                     v-model.number="currentNoteWidth">
            </div>
          </div>
        </div>
      </div>
      <div class="field is-horizontal">
        <div class="field-label is-normal">
          <label class="label">scroll:</label>
        </div>
        <div class="field-body">
          <div class="field">
            <div class="control">
              <input class="input-range is-primary" type="range" min="1"
                     :max="this.scoreArray.length"
                     v-model.number="currentBarIndex">
            </div>
          </div>
        </div>
      </div>
    </div>

    <div id="horizontal-tab">
      {{/* 弦 */}}
      <svg class="horizontal-tab-string" v-for="string in [1,2,3,4,5,6]" :viewBox="consts['VIEWBOX']"
           :height="consts['HEIGHT']" :width="consts['WIDTH']">
        <line x1="0" :x2="currentBarWidth * scoreArray.length + 1"
              :y1="string * consts['STRING_INTERVAL'] + consts['STRING_OFFSET']"
              :y2="string * consts['STRING_INTERVAL'] + consts['STRING_OFFSET']"></line>
      </svg>

      {{/* ここがメインの譜面 */}}
      <div class="horizontal-tab-score">
        <div v-for="bar in scoreArray" :key="bar.index">

          {{/* 1小節中の音符配列が bar['notes'] */}}
          {{/* notes には { 2: "B", 6: "F" } の形で入る */}}
          <div class="horizontal-tab-bar-notes">
            <div class="horizontal-tab-notes" v-for="(notes, index) in bar['notes']" :key="index">

            {{/* 小節線も可変 + 番号 */}}
            <svg v-if="(bar.index * beats + index)" class="horizontal-tab-bar-line" :viewBox="viewBox">
              <text :x="bar.index * currentBarWidth - 5" y="55">{{bar.index}}</text>
              <line :x1="bar.index * currentBarWidth" y1=75 :x2="bar.index * currentBarWidth" y2=225></line>
            </svg>


              {{/* ex.) note: "B", string: 2 */}}
              <div class="horizontal-tab-note" v-for="(note, string) in notes">
                <Note :passed-view-box="viewBox"
                      :x="bar.index * currentBarWidth + (index + 0.5) * currentNoteWidth"
                      :y="string * consts['STRING_INTERVAL'] + consts['STRING_OFFSET']"
                      :r="consts['NOTE_RADIUS']"
                      :pitch="note"
                      :nth="parseInt(string, 10)"
                      :capo="capo"
                      :tuning="tuning">
                </Note>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Note from './fragments/Note';

  export default {
    components: {
      Note,
    },
    props: {
      scoreArray: Array,
      beats: Number,
      position: String,
      tuning: String,
      capo: Number,
    },
    data: function () {
      return {
        consts: {
          VIEWBOX: "0 0 1200 300",
          HEIGHT: 300,
          WIDTH: 1200, // 画面幅に合わせたい
          STRING_INTERVAL: 30,
          STRING_OFFSET: 45,
          BAR_WIDTH: this.beats * 42,
          NOTE_RADIUS: 15,
        },
        currentBarIndex: 1,
        currentNoteWidth: 42,
      }
    },
    computed: {
      /**
       * 現在の小節番号に従ってviewBoxの位置を変更する
       * @returns {string}
       */
      viewBox: function () {
        return `${this.currentBarIndex * this.currentNoteWidth * this.beats - 20} 0 1200 300`;
      },

      currentBarWidth: function () {
        return this.currentNoteWidth * this.beats;
      }
    },
  }
</script>
<style scoped>
  svg {
    position: absolute;
    width: 100%;
    height: 100%;
  }

  #horizontal-tab {
    background-color: aliceblue;
    height: 300px;
    position: relative;
  }

  .horizontal-tab-controller {
    margin: 10px 0;
  }
  /* bulma標準でサポートしていない */
  .input-range[type="range"] {
    background-color: #eaeaea;
    height: 2px;
    width: 100%;
    border-radius: 6px;
  }

  .horizontal-tab-string {
    stroke: darkgray;
    stroke-width: 1.5;
    fill: none;
  }

  .horizontal-tab-bar-line line {
    stroke: royalblue;
    stroke-dasharray: 5, 5;
    stroke-width: 1;
    fill: none;
  }

  .horizontal-tab-bar-line text {
    stroke: none;
    fill: royalblue;
    font-size: 1.2rem;
  }
</style>
