<script setup lang="ts">
import { ArrowLeft } from 'lucide-vue-next'
import { useCarousel } from './useCarousel'
import type { WithClassAsProps } from './interface'
import { cn } from '@/lib/utils'
import { Button } from '@/components/ui/button'

const props = defineProps<WithClassAsProps>()

const { orientation, canScrollPrev, scrollPrev } = useCarousel()
</script>

<template>
  <Button
    :disabled="!canScrollPrev"
    :class="cn(
      'touch-manipulation absolute h-9 w-9 rounded-full p-0',
      orientation === 'horizontal'
        ? '-left-4 top-1/2 -translate-y-1/2 opacity-30 hover:opacity-100 transition-all'
        : '-top-12 left-1/2 -translate-x-1/2 rotate-90',
        !canScrollPrev ? 'hidden' : '',
      props.class,
    )"
    variant="outline"
    @click="scrollPrev"
  >
    <slot>
      <ArrowLeft class="h-4 w-4 text-current" />
      <span class="sr-only">Previous Slide</span>
    </slot>
  </Button>
</template>
