<script setup lang="ts">
import { getIpfsUrl } from '@/helpers/utils';

defineProps<{
  open: boolean;
  authorIpfsHash: string;
  relayerIpfsHash?: string;
}>();
defineEmits(['close']);
</script>

<template>
  <BaseModal :open="open" @close="$emit('close')">
    <template #header>
      <h3>{{ $t('receipt') }}</h3>
    </template>
    <div class="m-4 space-y-4">
      <BaseBlock slim class="p-4 text-skin-link">
        <div class="flex">
          <span class="mr-1 flex-auto text-skin-text" v-text="$t('author')" />
          <BaseLink :link="getIpfsUrl(authorIpfsHash)" class="text-skin-link">
            #{{ authorIpfsHash.slice(0, 7) }}
          </BaseLink>
        </div>
        <div v-if="relayerIpfsHash" class="flex">
          <span class="mr-1 flex-auto text-skin-text" v-text="$t('relayer')" />
          <BaseLink :link="getIpfsUrl(relayerIpfsHash)" class="text-skin-link">
            #{{ relayerIpfsHash.slice(0, 7) }}
          </BaseLink>
        </div>
      </BaseBlock>
      <BaseLink
        :link="`https://signator.io/view?ipfs=${authorIpfsHash}`"
        class="mb-2 block"
        hide-external-icon
      >
        <BaseButton tabindex="-1" class="w-full">
          {{ $t('verifyOnSignatorio') }}
          <i-ho-external-link class="mb-[2px] ml-1 inline-block text-xs" />
        </BaseButton>
      </BaseLink>
    </div>
  </BaseModal>
</template>
