<style>
div {
  padding: 10px 0;
}
.team-logo {
  max-width: 150px;
  display: block;
  max-height: 110px;
}
.team-score {
  font-size: 25px;
  font-weight: 600;
}
.name {
  font-size: 18px;
  font-weight: 600;
}
</style>
<template>
<div class="team-score">{{team.score}}</div>
    <img :src="team.teamLogo" class="team-logo">
    <div class="name">{{team.name}}</div>
</template>

<script>
export default {
  props: ['team'],
}
</script>