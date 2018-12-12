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
              <input class="input" type="number" v-model="capo">
            </div>
          </div>
        </div>
      </div>
      <div class="field is-horizontal">
        <div class="field-label is-normal">
          <label class="label">beats:</label>
        </div>
        <div class="field-body">
          <div class="field">
            <div class="control">
              <input class="input" type="number" v-model="beats">
            </div>
          </div>
        </div>
      </div>
    </div>

    {{/* 譜面スクロール用slider */}}
    <vue-slider id="horizontal-slider" ref="slider"
                v-model="currentBarIndex"
                :min="1"
                :max="this.scoreArray.length"
                :style="'{display: inline-block}'" />

    <div id="horizontal-tab">
      {{/* 弦 */}}
      <svg class="horizontal-tab-string" v-for="string in [1,2,3,4,5,6]" :viewBox="consts['VIEWBOX']"
           :height="consts['HEIGHT']" :width="consts['WIDTH']">
        <line x1="0" :x2="consts['BAR_WIDTH'] * scoreArray.length + 1"
              :y1="string * consts['STRING_INTERVAL'] + consts['STRING_OFFSET']"
              :y2="string * consts['STRING_INTERVAL'] + consts['STRING_OFFSET']"></line>
      </svg>

      {{/* ここがメインの譜面 */}}
      <div class="horizontal-tab-score">
        <div v-for="bar in scoreArray" :key="bar.index">

          {{/* 小節線 + 番号 */}}
          <svg class="horizontal-tab-bar-line" :viewBox="viewBox">
            <text :x="bar.index * consts['BAR_WIDTH'] - 5" y="55">{{bar.index}}</text>
            <line :x1="bar.index * consts['BAR_WIDTH']" y1=75 :x2="bar.index * consts['BAR_WIDTH']" y2=225></line>
          </svg>

          {{/* 1小節中の音符配列が bar['notes'] */}}
          {{/* notes には { 2: "B", 6: "F" } の形で入る */}}
          <div class="horizontal-tab-bar-notes">
            <div class="horizontal-tab-notes" v-for="(notes, index) in bar['notes']" :key="index">

              {{/* ex.) note: "B", string: 2 */}}
              <div class="horizontal-tab-note" v-for="(note, string) in notes">
                <Note :passed-view-box="viewBox"
                      :x="bar.index * consts['BAR_WIDTH'] + (index + 0.5) * consts['NOTE_WIDTH']"
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
  import vueSlider from 'vue-slider-component'
  import Note from './fragments/Note';

  export default {
    components: {
      vueSlider,
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
          BAR_WIDTH: 210,
          NOTE_WIDTH: 210 / this.beats,
          NOTE_RADIUS: 15,
        },
        currentBarIndex: 1,
      }
    },
    computed: {
      /**
       * 現在の小節番号に従ってviewBoxの位置を変更する
       * @returns {string}
       */
      viewBox: function () {
        return `${this.currentBarIndex * this.consts['BAR_WIDTH'] - 20} 0 1200 300`;
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
