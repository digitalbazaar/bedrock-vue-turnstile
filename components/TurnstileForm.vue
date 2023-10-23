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

<script setup>
/*!
  * Copyright (c) 2023 Digital Bazaar, Inc. All rights reserved.
  */
import {defineEmits, defineProps, ref, watch} from 'vue';
import {config} from '@bedrock/web';
import VueTurnstile from 'vue-turnstile';

defineProps({
  modelValue: {
    type: String,
    required: true,
  },
  resetInterval: {
    default: 295000,
    type: Number,
    required: false,
  },
  size: {
    default: 'normal',
    type: String,
    required: false,
  },
  theme: {
    default: 'auto',
    type: String,
    required: false,
  },
  action: {
    default: '',
    type: String,
    required: false,
  },
  appearance: {
    default: 'always',
    type: String,
    required: false,
  },
  renderOnMount: {
    default: true,
    type: Boolean,
    required: false,
  }
});

const token = ref('');
// siteKey is not a secret
const siteKey = ref(config.turnstile.siteKey);

const emit = defineEmits(['update:modelValue']);
watch(token, tokenValue => emit('update:modelValue', tokenValue));

</script>
