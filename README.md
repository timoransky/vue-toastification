# Vue Toastification with custom component

This package is built on top of [Vue Toastification](https://maronato.github.io/vue-toastification/) with the ability to use custom component for notification item.

Light, easy and beautiful toasts!

Wanna try it out? Check out the [live demo](https://demo.craftable.pro) of our Craaftable PRO Laravel admin panel!

**Attention!** This package is **only** compatible with Vue 3+

For full docs please see original package [Vue Toastification](https://maronato.github.io/vue-toastification/)

# Create custom Vue notification component

Your custom notification component has to use `VtToast` component which has defined slot props.
It can look like this:

```vue
<template>
  <VtToast
    v-slot="slotProps"
    class="group pointer-events-auto w-full max-w-sm overflow-hidden !rounded-lg !bg-white !shadow-lg ring-1 ring-black ring-opacity-5"
  >
    <div class="w-full">
      <div class="flex items-start">
        <div class="mr-3 flex-shrink-0">
          <CheckCircleIcon
            v-if="slotProps.type === 'success'"
            class="h-6 w-6 text-success-500"
            aria-hidden="true"
          />
          <ExclamationCircleIcon
            v-else-if="slotProps.type === 'warning'"
            class="h-6 w-6 text-warning-500"
            aria-hidden="true"
          />
          <InformationCircleIcon
            v-else-if="slotProps.type === 'info'"
            class="h-6 w-6 text-info-500"
            aria-hidden="true"
          />
          <ExclamationCircleIcon
            v-else-if="slotProps.type === 'error'"
            class="h-6 w-6 text-danger-500"
            aria-hidden="true"
          />
          <BellIcon v-else class="h-6 w-6 text-gray-400" aria-hidden="true" />
        </div>
        <div class="w-0 flex-1 pt-0.5">
          <p class="text-sm font-medium text-gray-900">
            {{ slotProps.content }}
          </p>
          <p v-if="slotProps.description" class="mt-1 text-sm text-gray-500">
            {{ slotProps.description }}
          </p>
        </div>
        <div class="ml-4 flex flex-shrink-0">
          <button
            v-if="!!slotProps.closeButton"
            class="inline-flex rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-primary-500 focus:ring-offset-2"
            :class="{
              'opacity-0 hover:opacity-100 group-hover:opacity-50':
                slotProps.showOnHover,
            }"
            @click.stop="slotProps.closeToast"
          >
            <!-- TODO: translation here causes some errors -->
            <span class="sr-only">Close</span>
            <XMarkIcon class="h-5 w-5" aria-hidden="true" />
          </button>
        </div>
      </div>
    </div>
  </VtToast>
</template>

<script setup lang="ts">
import {
  ExclamationCircleIcon,
  CheckCircleIcon,
  InformationCircleIcon,
  XMarkIcon,
  BellIcon,
} from "@heroicons/vue/24/outline"
import { VtToast } from "@brackets/vue-toastification"
</script>
```

# Using custom Vue notification component

To use custom Vue component, simply pass `rootComponent` attribute into options object like this:

```javascript
import { createApp } from "vue";
import Toast from "vue-toastification";
import Notification from "my/custom/component";
// Import the CSS or use your own!
import "vue-toastification/dist/index.css";

const app = createApp(...);

const options = {
  rootComponent: Notification
};

app.use(Toast, options);
```

Or, if you are using Typescript:

```javascript
import { createApp } from "vue";
import Toast, { PluginOptions } from "vue-toastification";
import Notification from "my/custom/component";
// Import the CSS or use your own!
import "vue-toastification/dist/index.css";

const app = createApp(...);

const options: PluginOptions = {
  rootComponent: Notification
};

app.use(Toast, options);
```

# License

Copyright (C) 2020 [timoransky](https://github.com/timoransky). Licensed under MIT
