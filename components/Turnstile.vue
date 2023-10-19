<template>
  <vue-turnstile
    v-model="token"
    theme="light"
    appearance="interaction-only"
    :site-key="siteKey" />
</template>
<script>
/*!
  * Copyright (c) 2023 Digital Bazaar, Inc. All rights reserved.
  */
import {config} from '@bedrock/web';

export default {
  name: 'Turnstile',
  data() {
    return {
      // siteKey is not a secret
      siteKey: config.turnstile.siteKey
    }
  }
};

</script>
