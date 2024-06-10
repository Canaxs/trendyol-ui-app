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
</script>
<template>
<Sheet>
    <SheetTrigger as-child>
      <div class="flex">
      <Button variant="outline" class="p-5">
        <Icon name="ri:menu-fill" class="size-5 mr-1" />
      </Button>
      <div class="ml-3 relative top-1">
        <img src="https://cdn.dsmcdn.com/web/logo/ty-web.svg" alt="Trendyol Logo" width="100px" height="100px" />
      </div>
    </div>
    </SheetTrigger>
    <SheetContent side="left">
      <SheetHeader>
        <SheetTitle>Edit profile</SheetTitle>
        <SheetDescription>
          Make changes to your profile here. Click save when you're done.
        </SheetDescription>
      </SheetHeader>
      <div class="grid gap-4 py-4">
        <div class="grid grid-cols-4 items-center gap-4">
            Name
          <Input id="name" value="Pedro Duarte" class="col-span-3" />
        </div>
        <div class="grid grid-cols-4 items-center gap-4">
            Username
          <Input id="username" value="@peduarte" class="col-span-3" />
        </div>
      </div>
      <SheetFooter>
        <SheetClose as-child>
          <Button type="submit">
            Save changes
          </Button>
        </SheetClose>
      </SheetFooter>
    </SheetContent>
  </Sheet>
</template>