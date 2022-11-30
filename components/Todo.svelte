<script>
  export let savedNotes;
  let editedContent = "";

  function removeANote(idx) {
    savedNotes.splice(idx, 1);
    savedNotes = savedNotes;
  }

  function completeANote(idx) {
    savedNotes[idx].isCompleted = !savedNotes[idx].isCompleted;
  }

  function editANote(idx) {
    savedNotes[idx].isBeingEdited = !savedNotes[idx].isBeingEdited;
    if (savedNotes[idx].isBeingEdited === false) {
      if (editedContent !== "") {
        savedNotes[idx].content = editedContent;
        editedContent = "";
      }
    }
  }
</script>

{#each savedNotes as note, i}
  <ul>
    {#if note.isCompleted}
      <div class="noteWrapper">
        <li><s>Task {i + 1}: {note.content}</s></li>
      </div>
    {:else}
      <div class="noteWrapper">
        <li>Task {i + 1}: {note.content}</li>
        {#if note.isBeingEdited}
          <li>
            <input placeholder={`Edit your task`} bind:value={editedContent} />
          </li>
        {/if}
      </div>
    {/if}

    <button on:click={() => removeANote(i)}
      ><img src="assets/remove.png" alt="remove" /></button
    >
    <button on:click={() => completeANote(i)}
      ><img src="assets/check.png" alt="complete" /></button
    >
    <button on:click={() => editANote(i)}
      ><img src="assets/edit.png" alt="edit" /></button
    >
  </ul>
{/each}

<style>
  button {
    background-color: transparent;
    background-repeat: no-repeat;
    border: none;
    cursor: pointer;
    overflow: hidden;
    outline: none;
  }
  ul {
    list-style-type: none;
  }

  .noteWrapper {
    background-color: white;
    color: black;
    display: flex;
    align-items: center;
    width: auto;
    height: 50px;
    border: 1px white solid;
    border-radius: 10px;
  }
</style>
