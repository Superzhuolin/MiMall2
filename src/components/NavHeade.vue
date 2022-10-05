<template>
  <div class="header">
    header
  </div>
</template>

<script>
import { mapState } from "vuex";
export default {
  name: "nav-header",
  data() {
    return {
      phoneList: [],
    };
  },
};
</script> 
<style lang="scss">
@import "/src/assets/scss/base.scss";
@import "/src/assets/scss/mixin.scss";
@import "/src/assets/scss/config.scss";
</style>
