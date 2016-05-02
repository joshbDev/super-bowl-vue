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
<div class="header">Teams <small>listed by first appearance in a super bowl</small></div>
<div>
  <div v-for="sb in superBowlTeams" v-on:click="chooseTeam(sb.name)" v-bind:class="sb.class">{{sb.name}}</div>
</div>
</template>

<script>
import {sbData} from './sb-data';
import {uniq, flattenDeep} from 'lodash';

let superBowlTeamNames = [];
for (const sbName in sbData) {
  superBowlTeamNames.push(sbData[sbName].teams);
}
superBowlTeamNames = uniq(flattenDeep(superBowlTeamNames));

const superBowlTeams = superBowlTeamNames.map((team) => {
  return {
    name: team,
    class: 'clickable sb-titles',
  };
});


export default {
  data: () => {
    return {
      superBowlTeams,
    };
  },
  ready() {
    this.$watch('chosen-year', (oldVal, year) => {
      const yearObject = sbData[year];
      this.superBowlTeams.map((team) => {
        if(yearObject && (yearObject.teams[0] === team.name || yearObject.teams[1] === team.name)) {
          team.class = 'clickable chosen';
        } else {
          team.class = 'clickable';
        }
      });
    });
  },
  methods: {
    chooseTeam(team) {
      let chosenTeam = team;
      if (this.previouslyChosenTeam === chosenTeam) {
        chosenTeam = undefined;
      }
      this.superBowlTeams.map((mapTeam) => {
        if(mapTeam.name === chosenTeam) {
          mapTeam.class = 'clickable chosen sb-titles';
        } else {
          mapTeam.class = 'clickable sb-titles';
        }
      });
      this.previouslyChosenTeam = chosenTeam;
      this.$dispatch('team-chosen', chosenTeam);
    },
  },
};
</script>