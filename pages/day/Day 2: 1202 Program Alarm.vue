<template>
  <section class="section">
    <div class="columns is-desktop is-multiline">
      <div class="column is-full">
        <ChallengeTitle title="1202 Program Alarm"
                        subtitle="Day 2"
                        link="https://adventofcode.com/2019/day/2"/>
      </div>

      <div class="column is-8-desktop">
        <b-field label="Source Data">
          <b-input type="textarea" v-model="inputData"></b-input>
        </b-field>

            <div class="columns is-mobile">
              <div class="column">
                <b-field label="Answer 1">
                  <b-input type="text" v-model="partOne"></b-input>
                </b-field>
              </div>
              <div class="column">
                <b-field label="Answer 2">
                  <b-input type="text" v-model="partTwo"></b-input>
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
        srcData: '1,0,0,3,1,1,2,3,1,3,4,3,1,5,0,3,2,1,9,19,1,10,19,23,2,9,23,27,1,6,27,31,2,31,9,35,1,5,35,39,1,10,39,43,1,10,43,47,2,13,47,51,1,10,51,55,2,55,10,59,1,9,59,63,2,6,63,67,1,5,67,71,1,71,5,75,1,5,75,79,2,79,13,83,1,83,5,87,2,6,87,91,1,5,91,95,1,95,9,99,1,99,6,103,1,103,13,107,1,107,5,111,2,111,13,115,1,115,6,119,1,6,119,123,2,123,13,127,1,10,127,131,1,131,2,135,1,135,5,0,99,2,14,0,0',
        // perm: [[12,2]]
        perm: this.permutate2Arrays(this.range(100),this.range(100))
      }
    },
    computed: {
      partOne() {
        // return 'num'
        let arr = this.inputData.split(',').map(x => Number(x));
        return !!this.inputData ? this.intcode(this, arr, 0, 12, 2)[0] : ''
      },
      partTwo() {
        if (!this.inputData) return ''
        
        let self = this;
        const oldArr = this.inputData.split(',').map(x => Number(x));

        for (let i = 0; i < this.perm.length; i++){
          let arr = [...oldArr]
          let res = this.intcode(this, arr, 0, this.perm[i][0], this.perm[i][1])[0]

          if (res == 19690720) {
            return this.perm[i][0] + '' + this.perm[i][1]
          }
        }

        return 'stuff'
      }
    },
    methods: {
      range: int => {
        return [...Array(int).keys()]
      },
      permutate2Arrays: (array1, array2) => {
          let resultArray = []
          
          for (var i = 0; i < array1.length; i++) {
              for (var j = 0; j < array2.length; j++) {
                var tempArray = [];
                tempArray.push(array1[i]);
                tempArray.push(array2[j]);
                resultArray.push(tempArray);
              }
            }
            
            for (var i = 0; i < array2.length; i++) {
              for (var j = 0; j < array1.length; j++) {
                var tempArray = [];
                tempArray.push(array1[j]);
                tempArray.push(array2[i]);
                resultArray.push(tempArray);
              }
            }

          return resultArray
      },
      intcode: (self, internalArr, index, swap1, swap2) => {
        if (!!swap1) internalArr[1] = Number(swap1)
        if (!!swap2) internalArr[2] = Number(swap2)
        
        let pos1 = internalArr[index + 1],
            pos2 = internalArr[index + 2],
            pos3 = internalArr[index + 3];

        if (internalArr[index] == 1) {
          internalArr[pos3] = internalArr[pos1] + internalArr[pos2]
        } else if (internalArr[index] == 2) {
          internalArr[pos3] = internalArr[pos1] * internalArr[pos2]
        }
        
        return (internalArr[index + 4] == 99) ? internalArr : self.intcode(self, internalArr, index + 4)
      }
    }
  }
</script>
