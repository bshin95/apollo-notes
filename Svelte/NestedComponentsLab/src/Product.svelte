<script>
  import { createEventDispatcher } from 'svelte' //createEventDispatcher is a built-in method from svelte

  export let title; //these two are props
  export let price;
  export let bestseller = false; //you can tell svelte this is an optional prop like this

  const dispatch = createEventDispatcher();

  function addToCart() {
    dispatch('add-to-cart', {id: 'p1'})
  }
</script>

<article>
  <h1>{title}</h1>
  <h2>${price}</h2>
  {#if bestseller}
    <h3>Best seller</h3>
  {/if}
  <button on:click="{addToCart}">Add to cart</button>
  <!-- if you leave the event listener empty, the function is handled in the app.svelte file -->
  <button on:click="{() => {dispatch('delete')}}">Delete</button>
  <!-- the add to cart and delete button perform the same exact function, except the delete button is just written as an inline function because it is simple. -->
</article>