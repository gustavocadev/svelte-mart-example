<script lang="ts">
  import type { CartProduct, Product } from '$lib/types';
  import Minus from 'phosphor-svelte/lib/Minus';
  import Plus from 'phosphor-svelte/lib/Plus';
  import Trash from 'phosphor-svelte/lib/Trash';

  interface Props {
    product: CartProduct;
    removeFromCart: (id: string) => void;
  }

  let { product = $bindable(), removeFromCart }: Props = $props();
</script>

<div class="flex items-center justify-between py-2 border-b border-gray-200">
  <div class="flex items-center">
    <img
      src={product.product.thumbnail}
      alt="Product"
      class="size-12 object-cover rounded mr-4"
    />
    <div>
      <p class="font-medium">{product.product.title}</p>
      <p class="text-sm">${product.product.price} each</p>
    </div>
  </div>
  <div class="flex items-center">
    <button
      class={`p-1 hover:bg-gray-200 rounded`}
      aria-label="Subtract 1 from quantity"
      onclick={() => {
        if (product.quantity > 1) {
          product.quantity--;
          return;
        }
        removeFromCart(product.id);
      }}
    >
      <Minus class="size-4" />
    </button>
    <span class="mx-2">{product.quantity}</span>
    <button
      class="p-1 hover:bg-gray-200 rounded"
      aria-label="Add 1 to quantity"
      onclick={() => {
        product.quantity++;
      }}
    >
      <Plus class="size-4" />
    </button>
    <button
      class="ml-4 p-1 text-red-500 hover:bg-red-100 rounded"
      onclick={() => {
        removeFromCart(product.id);
      }}
    >
      <Trash class="size-4" />
    </button>
  </div>
</div>
