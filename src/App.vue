<template>
  <Header />
  <div class="container">
    <Balance />
  </div>
</template>

<script>
import Balance from './components/Balance.vue';
import Header from './components/Header.vue';

export default {
  components: {
    Header,
    Balance
  }
}
</script>