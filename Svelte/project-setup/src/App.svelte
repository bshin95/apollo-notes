<script>
import { bubble } from "svelte/internal";
  import ContactCard from "./ContactCard.svelte";

  let name = "Max";
  let title = "";
  let image = "";
  let description = "";
  let formState = 'empty';

  let createdContacts = [];

  function addContact() {
    if (
      name.trim().length == 0 || 
      title.trim().length == 0 || 
      image.trim().length == 0 || 
      description.trim().length == 0
    ) { //trim gets rid of the whitespaces
      formState = 'invalid';
      return;
    }
    creactedContacts = [...createdContacts, {id: Math.random(), name: name, jobTitle: title, imageUrl: image, desc: description}] //the spread operator will pull out all the elements out of createdContacts and adds them to a new array and adds the new object to the end of the array after the old elements of the array are pulled out
    //the equal sign overwrites the old elements
    formState = 'done';
  }

  function deleteFirst() {
    createdContacts = createdContacts.slice(1) //takes createdContacts and gives us a new array and removes the first index or the [0] index
  }

  function deleteLast() {
    createdContacts = createdContacts.slice(0, -1); //gives us a new array starting at the first index of the array, but removes the last index
  }
</script>

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>

<div id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={title} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={image} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
</div>

<button on:click={addContact}>Add Contact Card</button>
<!-- if the button was in a form, you would want to do to on:click|preventDefault which is the same as event prevent default which will stop the page from reloading after the button is submitted -->

<button on:click={deleteFirst}>Delete first</button>
<button 
  on:click="{(event) => 
    {createdContacts = createdContacts.slice(1)
  }}">
  Delete First
</button>
<!-- if the logic of the button is short and simple, you can just define it as an line function. the two buttons above perform the same function, except the function of the first delete button is defined above in the script, while the second button's logic is defined as an inline function -->

<button on:click={deleteLast}>Delete last</button>

{#if formState === 'invalid'}
  <p>Invalid input.</p>
{:else}
  <p>Please enter some data and hit the button.</p>
{/if}

{#each createdContacts as contact, i (contact.id)} 
<h2># {i + 1}</h2>
<!-- allows us to loop through an array -->
<ContactCard 
  name={contact.name} 
  jobTitle={contact.jobTitle} 
  description={contact.desc} 
  userImage={contact.imageUrl} 
/>
{:else}
  <p>Please start adding some contacts, we found none!</p>
{/each}