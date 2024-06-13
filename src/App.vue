<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import SVPlot from './components/SVPlot.vue'
</script>

<template>
  <nav>
    <span>Navigation|</span>
    <span>Place|</span>
    <span>Holder</span>
  </nav>
  <main id="main-content">
    <SVPlot />
  </main>
  <div class="info__main">
    Summary Stats Placeholder
    <pre>
      chr1    50186563
      DUP_1:50186563-50186750 T
      PASS
      END=50186750
      SVTYPE=DUP
      SVLEN=188
      AC=65
      NS=120471
      CALLRATE=0.85
      AF=0.000274
      PRE=1.04,0.078720
      POST=1.04,0.078583
      DPCNT=1.003,0.000:0.010,0.000,0.000:1.000::1.518,0.361:0.012,0.001,0.014:0.000
      DPCNToverlap=0.000
      Biallelic
      SPLIT=50186563,50186751
      GCPCT=43
      GTCNT=20658,120405,66,0
      AN=236006
      MUCNVQ=50
    </pre>
  </div>
  <div class="info__extra">
    Dynamic Info Placeholder
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
