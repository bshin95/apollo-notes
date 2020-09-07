<script>
import App from "../../project-setup/src/App.svelte";
import ContactCard from "../../project-setup/src/ContactCard.svelte";
import SvetleSyntax from "../../SvelteNotes/SvetleSyntax.svelte";
import Product from "./Product.svelte"
import Modal from "./Modal.svelte"

import { tick } from 'svelte'

let text = 'dummy text'

  products = [
    {
      id: 'p1',
      title: 'A Book',
      price: 9.99
    }
  ]; //it is important to make sure the name of the object in the array matches how the prop is being passed down in the product.svelte file

  function addToCart(event) {
    console.log(event);
  }

  function deleteProduct(event) {
    console.log(event)
  }

  function transform() {
    if (event.which !== 9) {
      return
    }
    event.preventDefault();

    const selectionStart = event.selectionStart
    const selectionEnd = event.selectionEnd
    const value = event.target.value

    text = value.slice(0, selectionStart) + 
      value.slice(selectionStart, selectionEnd).toUpperCase() + 
      value.slice(selectionEnd);

      tick().then(() => { //must use tick, you use very rarely
        event.target.selectionStart = selectionStart;
        event.target.selectionEnd = selectionEnd;
      })
    //code will not work
    // event.target.selectionStart = selectionStart;
    // event.target.selectionEnd = selectionEnd;
  }
</script>

<!-- this loop is iterating through the products array above in the script and saves it as 'product'. the title and price is now passing in the arrays title and price -->
{#each products as product}
<!-- the product.svelte file is taking the title and price above as props -->
<!-- instead of passing the title and price as title={product.title} and price={product.price}, you can use the spread operator like {...product}, this will pass everything in the products array into the product component. -->
<!-- You can pass down props that aren't defined because you are not using them, so in this case, we are not using id but it is being passed down -->
<!-- title={product.title}
  price={product.price} -->
<Product 
  {...product}
  on:add-to-cart={addToCart}
  on:delete={deleteProduct}
/>
{/each}
<!-- svelte will see that the two event listeners are using add-to-cart and delete, which will reference to the Product.svelte file and find the dispatch -->
<!-- the two event listeners are now listening to the functions above, which is expected to console log the event details. and in this instance, we passed in the id of "p1" as a data when the button is clicked -->

<Modal>
  <h1 slot="header">Hello!</h1>
  <p>This works!</p>
</Modal>
<!-- the h1 tag will take in the slot that is named header, while the p tag will render on the default slot -->

<textarea rows="5" value={text} on:keydown={transform}></textarea>