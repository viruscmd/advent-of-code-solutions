<template>
  <section class="section">
    <div class="columns is-desktop is-multiline">
      <div class="column is-full">
        <ChallengeTitle title="The Tyranny of the Rocket Equation"
                        subtitle="Day 1"
                        link="https://adventofcode.com/2019/day/1"/>
      </div>

      <div class="column is-8-desktop">
        <b-field label="Source Data">
          <b-input type="textarea" v-model="inputData"></b-input>
        </b-field>

        <div class="columns is-touch">
          <div class="column is-half">
            <b-field label="Answer 1">
              <b-input type="number" v-model="partOne"></b-input>
            </b-field>
          </div>

          <div class="column is-half">
            <b-field label="Answer 2">
              <b-input type="number" v-model="partTwo"></b-input>
            </b-field>
          </div>
        </div>
      </div>

      <div class="column">
        <b-field type="textarea" label="Source Data">
          <b-input type="textarea" disabled v-model="srcData"></b-input>
        </b-field>

        <b-field>
          <p class="control">
            <b-button @click="inputData = srcData" type="is-primary" expanded>Use Source Data</b-button>
          </p>
        </b-field>
      </div>
    </div>
  </section>
</template>

<script>
  import ChallengeTitle from '~/components/ChallengeTitle';
  export default {
    name: 'Day1',
    components: {
      ChallengeTitle
    },
    data() {
      return {
        inputData: '',
        srcData: '112908\n' +
          '61769\n' +
          '65967\n' +
          '51494\n' +
          '99689\n' +
          '114098\n' +
          '135346\n' +
          '59561\n' +
          '147324\n' +
          '50465\n' +
          '117491\n' +
          '77845\n' +
          '91959\n' +
          '59847\n' +
          '84013\n' +
          '85763\n' +
          '62121\n' +
          '58965\n' +
          '89809\n' +
          '97870\n' +
          '77696\n' +
          '70218\n' +
          '118404\n' +
          '83505\n' +
          '141729\n' +
          '61534\n' +
          '101073\n' +
          '131358\n' +
          '76104\n' +
          '120836\n' +
          '109789\n' +
          '96510\n' +
          '65406\n' +
          '117906\n' +
          '74921\n' +
          '95412\n' +
          '99875\n' +
          '134298\n' +
          '105235\n' +
          '82802\n' +
          '103392\n' +
          '81906\n' +
          '133786\n' +
          '140681\n' +
          '109004\n' +
          '148434\n' +
          '92333\n' +
          '83848\n' +
          '98297\n' +
          '95728\n' +
          '138202\n' +
          '79312\n' +
          '55633\n' +
          '138461\n' +
          '50293\n' +
          '141922\n' +
          '140303\n' +
          '66542\n' +
          '50054\n' +
          '99076\n' +
          '143201\n' +
          '66702\n' +
          '133583\n' +
          '70308\n' +
          '146824\n' +
          '95606\n' +
          '63054\n' +
          '129272\n' +
          '133051\n' +
          '58626\n' +
          '119896\n' +
          '66265\n' +
          '99925\n' +
          '131752\n' +
          '74669\n' +
          '148387\n' +
          '132124\n' +
          '107188\n' +
          '55535\n' +
          '145004\n' +
          '78122\n' +
          '50885\n' +
          '70325\n' +
          '100859\n' +
          '86484\n' +
          '88795\n' +
          '148164\n' +
          '64473\n' +
          '143089\n' +
          '121023\n' +
          '52904\n' +
          '120927\n' +
          '87164\n' +
          '133709\n' +
          '89427\n' +
          '105350\n' +
          '106378\n' +
          '98492\n' +
          '78394\n' +
          '145200'
      }
    },
    computed: {
      partOne() {
        return !!this.inputData ? this.inputData.split('\n').map(x => Math.floor(x / 3) - 2).reduce((a, b) => a + b, 0) : 0
      },
      partTwo() {
        return !!this.inputData ? this.inputData.split('\n').map(x => {
          let fuel = (y) => {
            let required = Math.floor(y / 3) - 2;
            return (required >= 0) ? required + fuel(required) : 0
          };

          return fuel(x)
        }).reduce((a, b) => a + b, 0) : 0
      }
    }
  }
</script>
