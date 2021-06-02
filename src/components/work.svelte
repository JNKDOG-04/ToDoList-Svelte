<script>
  let tasks = [];
  let taskTodo = '';

  function addTask(event){
    if(event.key === 'Enter'){
      const doTask = {
        name : taskTodo,
        action: false
      }
      tasks.push(doTask);
      tasks = tasks;
      taskTodo = '';
    }
  }

  function deleteTask(i){
    tasks.splice(i,1);
    tasks = tasks;
  }

  function updateTask(task, i){
    tasks[i].action = !task.action;
  }
</script>
<div>
  <div class="container mt-5">
    <div class="row">
      <div class="col-lg-8 offset-lg-2">
        <input type="text" class="form-control form-control-lg"
        on:keydown={addTask}
        bind:value={taskTodo} 
        placeholder="Write your task">
        <br>
      </div>

      <div class="col-lg-6 offset-lg-3">
        {#if tasks.length === 0}
          <div class="card p-2">
            <h5>No tasks at the moment, 😶 set a task.</h5>
          </div>
        {/if}

        <ul class="list-group">
              {#each tasks as task, i}
                <li class="list-group-item d-flex justify-content-between">
                    <span class={task.action === true ? 'text-success cursor' : 'cursor'} on:click={() => updateTask(task, i)}>
                        <i class={task.action === true ? 'fas fa-check-circle' : 'far fa-circle'} ></i>
                    </span>
                        <h5>{ task.name }</h5>
                    <span class="cursor text-danger" on:click={() => deleteTask(i)}>
                        <i class="fas fa-trash-alt"></i>
                    </span>
                </li>
              {/each}
        </ul>
      </div>
    </div>
  </div>
</div>
<style>
  .form-control-lg{
    font-size: 1.8rem;
  }
  input,h5{
    text-align: center;
  }

  .cursor{
    cursor: pointer;
  }
</style>