<template>
  <base-card>
    <form>
      <h3 class="text-center mb-3">Forgot Password</h3>

      <div class="form-group mb-3">
        <label class="mb-1">Email address</label>
        <input type="email" class="form-control form-control-lg" />
      </div>

      <button type="submit" class="btn btn-dark btn-lg" style="width:100%">
        Reset password
      </button>
    </form>
  </base-card>
</template>

<script>
import BaseCard from '@/components/BaseCard.vue';

export default {
  components: {
    BaseCard,
  },
};
</script>
