<template>
    <section class="score">
      Jogador<span>{{ this.correctCount }}</span> x 
     <span>{{ this.wrongCount }}</span> Computador
    </section>
</template>

<script>

export default {

  props: ['correctCount', 'wrongCount']
}

</script>

<style lang="scss">
.score {
  border-bottom: 1px solid black;
  padding: 24px;
  font-size: 18px;

  span {
    margin: 0 8px;
    padding: 8px;
    font-weight: bold;
    border: 1px solid black;
  }
}

</style>
