<template>
  <div class="home">
    <PkmnList :id="151" :offset="0" />
  </div>
</template>

<script>
import PkmnList from "../components/PkmnList";
export default {
  name: "Home",
  components: {
    PkmnList,
  },
};
</script>
