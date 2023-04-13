<script>
  let newTask = "";
  let tasks = [];

  function addTask() {
    if (newTask.trim() !== "") {
      tasks = [...tasks, { id: Date.now(), text: newTask.trim(), done: false }];
      newTask = "";
    }
  }

  function removeTask(id) {
    tasks = tasks.filter(task => task.id !== id);
  }
</script>

<main class="min-h-screen bg-gray-100 py-12 px-4 sm:px-6 lg:px-8">
  <div class="max-w-md mx-auto bg-white rounded-lg shadow-lg p-6">
    <h1 class="text-3xl font-bold mb-4">ToDo App</h1>
    <div class="flex">
      <input
        type="text"
        placeholder="Enter new task"
        bind:value="{newTask}"
        on:keyup="{e => e.key === 'Enter' && addTask()}"
        class="flex-1 border border-gray-300 rounded-lg p-2 mr-2"
      />
      <button on:click="{addTask}" class="bg-blue-500 text-white rounded-lg px-4 py-2">Add Task</button>
    </div>
    <ul class="mt-4">
      {#each tasks as task (task.id)}
        <li class="flex justify-between items-center py-2 px-4 my-2 border border-gray-300 rounded {task.done ? 'line-through' : ''}">
          <input
            type="checkbox"
            bind:checked="{task.done}"
            class="mr-2"
          />
          <span class="flex-1">{task.text}</span>
          <button class="text-red-500" on:click="{() => removeTask(task.id)}">Remove</button>
        </li>
      {/each}
    </ul>
  </div>
</main>
