<script setup lang="ts">
import {
  Sheet,
  SheetClose,
  SheetContent,
  SheetDescription,
  SheetFooter,
  SheetHeader,
  SheetTitle,
  SheetTrigger,
} from '@/components/ui/sheet';
import { Button } from '@/components/ui/button';
import ChildMenu from '~/data/ChildMenu';
import Side from '../Side-Menu/Side.vue';

const childMenu = ChildMenu;

</script>
<template>
<Sheet>
    <SheetTrigger as-child>
      <div class="flex">
      <Button variant="outline" class="p-5">
        <Icon name="ri:menu-fill" class="size-5 mr-1" />
      </Button>
      <div class="ml-3 relative top-1">
        <a href="/" ><img src="https://cdn.dsmcdn.com/web/logo/ty-web.svg" alt="Trendyol Logo" width="100px" height="100px" /></a>
      </div>
    </div>
    </SheetTrigger>
    <SheetContent side="left">
      <Side />
    </SheetContent>
  </Sheet>
</template>