<template>
    <section class="score">
      Jogador<span>{{ this.win_count }}</span> x 
     <span>{{ this.lose_count }}</span> Computador
    </section>
</template>

<script>

export default {
   
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
