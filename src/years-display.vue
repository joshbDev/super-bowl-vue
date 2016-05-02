<style>
.sb-titles {
  display: inline-block;
  margin: 10px;
  font-size: 15px;
  -webkit-transition: all .3s linear;
  -moz-transition: all .3s linear;
  -ms-transition: all .3s linear;
  -o-transition: all .3s linear;
  transition: all .3s linear;
}
.sb-titles:hover {
  color: #666;
  font-size: 17px;
}
.header {
    display: block;
    font-size: 40px;
}
small {
  font-size: 20px;
  color: #666;
}
.chosen {
  font-weight: 600;
  font-size: 23px;
}
</style>
<template>
<div class="header">Year</div><div v-for="sb in superBowlYears" class="sb-titles">
    <div v-on:click="chooseYear($index)" v-bind:class="sb.class">{{sb.name}}</div></div>
</template>
<script>
import {sbData} from './sb-data';
let previouslyChosenIndex;
const superBowlYears = [];
for (const sbName in sbData) {
  const dataToPush = sbData[sbName];
  dataToPush.name = sbName;
  dataToPush.class = 'clickable sb-titles';
  superBowlYears.push(dataToPush);
}
export default {
  data: () => {
    return {
      superBowlYears,
    }
  },
  methods: {
    chooseYear(index) {
      let chosenIndex = index;

      if (previouslyChosenIndex === chosenIndex) {
        chosenIndex = undefined;
      }
      superBowlYears.map((year, index) => {
        year.class = index === chosenIndex ? 'clickable chosen sb-titles' : 'clickable sb-titles';
      });
      const chosenObject = superBowlYears[chosenIndex];
      this.$dispatch('year-chosen', chosenObject && chosenObject.name);
      previouslyChosenIndex = index;
    }
  }

}
</script>
