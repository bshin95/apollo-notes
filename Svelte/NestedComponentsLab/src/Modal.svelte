<script>
  import { createEventDispatcher, onMount, onDestory, beforeUpdate, afterUpdate } from 'svelte'

  const dispatch = createEventDispatcher()

  let agreed = false;

  onMount(() => {
    console.log('onMount')
  })

  onDestory(() => {
    console.log('onDestory')
  })

  beforeUpdate(() =>{
    console.log('beforeUpdate')
  })

  afterUpdate(() => {
    console.log('afterUpdate')
  })
  
  console.log(('script executed'))
</script>

<div class="modal">
  <header>
    <slot name="header"/>
    <!-- this slot is named, so whichever html element takes in the named slot, it will render that -->
  </header>
  <div class="content">
    <slot/>
    <!-- however, this slot isn't named, which means this will be the default slot -->
  </div>
  <footer>
    <slot name="footer">
      <button>Close</button>
    </slot>
  </footer>
</div>