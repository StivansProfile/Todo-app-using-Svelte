<script>
  let noteContent = "";
  let notes = [];
  import Todo from "./Todo.svelte";

  function addNote() {
    if (noteContent !== "") {
      notes.push({
        content: noteContent,
        isCompleted: false,
        isBeingEdited: false,
      });
      notes = notes;
      noteContent = "";
    }
  }
</script>

<h1>Svelte To Do App</h1>
<input
  bind:value={noteContent}
  id="inputField"
  placeholder="write your task..."
/>
<button on:click={addNote} id="submitNote">Add a Task</button>

<Todo savedNotes={notes} />

<style>
  #inputField {
    width: 300px;
    height: 30px;
    font-size: large;
    border-radius: 10px;
  }

  #submitNote {
    width: 200px;
    height: 30px;
    border-radius: 10px;
    border: none;
    font-size: 15px;
    cursor: pointer;
  }
</style>
