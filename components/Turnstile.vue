<template>
  <VueTurnstile
    v-model="token"
    :reset-interval="resetInterval"
    :size="size"
    :theme="theme"
    :action="action"
    :appearance="appearance"
    :render-on-mount="renderOnMount"
    :site-key="siteKey" />
</template>
<script>
/*!
  * Copyright (c) 2023 Digital Bazaar, Inc. All rights reserved.
  */
import {config} from '@bedrock/web';
import {defineEmits, ref, watch} from 'vue';
import VueTurnstile from 'vue-turnstile';

export default {
  name: 'Turnstile',
  components: {VueTurnstile},
  props: {
    modelValue: {
      type: String,
      required: true,
    },
    resetInterval: {
      type: Number,
      required: false,
    },
    size: {
      type: String,
      required: false,
    },
    theme: {
      type: String,
      required: false,
    },
    action: {
      type: String,
      required: false,
    },
    appearance: {
      type: String,
      required: false,
    },
    renderOnMount: {
      type: Boolean,
      required: false,
    },
  },

  setup() {
    const token = ref('');
    // siteKey is not a secret
    const siteKey = ref(config.turnstile.siteKey);

    const emit = defineEmits(['update:modelValue'])
    watch(
      () => token.value,
      tokenValue => emit('update:modelValue', tokenValue));

    return {
      token,
      siteKey,
    }
  }
};

</script>
