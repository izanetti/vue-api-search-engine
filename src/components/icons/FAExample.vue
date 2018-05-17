<template>
  <span>
    <font-awesome-icon :icon="icon" />
  </span>
</template>

<script>
import FontAwesomeIcon from '@fortawesome/vue-fontawesome'
import faCoffee from '@fortawesome/fontawesome-free-solid/faCoffee'

export default {
  name: 'FAExample',

  computed: {
    icon() {
      return faCoffee
    }
  },

  components: {
    FontAwesomeIcon
  }
}
</script>