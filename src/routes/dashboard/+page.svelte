<script>
    let todoList = ['Do the groceries'];
    let currentTodo = '';
    let error = false;

    function addTodo() {
        error = false;
        if (!currentTodo){
            error = true;
        return;
        }
        todoList = [...todoList, currentTodo]
        currentTodo = "";
    }

    function editTodo(index){
        let newTodoList = [...todoList].filter((val, i) => {
            console.log(i, index, i !== index);
            return i !== index;
        });
        currentTodo = todoList[index]
        todoList = newTodoList
    }

    function removeTodo(index){
        let newTodoList = [...todoList].filter((val, i) => {
            console.log(i, index, i !== index);
            return i !== index;
        });
        todoList = newTodoList
    }
</script>

<div class="mainContainer">
    <div class="headerContainer">
        <h1>ToDo List</h1>
        <div class="headerButtons">
            <button><i class="fa-regular fa-floppy-disk"></i>Save</button>
            <button><i class="fa-solid fa-right-from-bracket"></i>Logout</button>
        </div>
    </div>
    <main>
        {#if todoList.length === 0}
        <p>
            You have nothing to do!
        </p>
        {/if}
        {#each todoList as todo, index}
            <div class="todo">
            <p>
                {index+1}. {todo}
            </p>
            <div class="actions">
                <i on:click={() => {editTodo(index)}} on:keydown={() => {}} class="fa-solid fa-pen-to-square"/>
                <i on:click={() => {removeTodo(index)}} on:keydown={() => {}} class="fa-regular fa-trash-can"></i>
            </div>
            </div> 
        {/each}   
    <main/>
    <div class={"enterTodo" + (error ? 'errorBorder' : "")}>
        <input bind:value={currentTodo} type="text" placeholder="Enter ToDo">
        <button on:click={addTodo}>Add</button>
    </div>
</div>

<style>
    .mainContainer{
        display: flex;
        flex-direction: column;
        min-height: 100vh;
        gap: 24px;
        padding: 24px;
        width: 100%;
        max-width: 1000px;
        margin: 0 auto;
    }
    
    .headerContainer{
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .headerButtons{
        display: flex;
        align-items: center;
        gap: 14px;
    }

    .headerContainer button{
        background: #003c5b;
        color: white;
        padding: 10px 18px;
        border: none;
        border-radius: 4px;
        font-weight: 700;
        display: flex;
        align-items: center;
        gap: 10px;
        cursor: pointer;
    }

    .headerContainer button i{
        font-size: 1.1rem;
    }

    .headerContainer button:hover{
        opacity: 0.7;
    }

    main{
        display: flex;
        flex-direction: column;
        gap: 8px;
        flex: 1;
    }

    .todo{
        border-left: 3px solid cyan;
        padding: 8px 14px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .actions{
        display: flex;
        align-items: center;
        gap: 14px;
        font-size: 1.3rem;
    }

    .actions i{
        cursor: pointer;
    }

    .actions i:hover{
        color: coral;
    }

    .enterTodo{
        display: flex;
        align-items: stretch;
        border: 1px solid #0891b2;
        border-radius: 5px;
        overflow: hidden;
    }

    .errorBorder{
        border-color: coral !important;
    }

    .enterTodo input{
        background: transparent;
        border: none;
        padding: 14px;
        color: white;
        flex: 1;
    }

    .enterTodo input:focus{
        outline: none;
    }

    .enterTodo button{
        padding: 0 28px;
        background: #003c5b;
        border: none;
        color: cyan;
        font-weight: 600;
        cursor: pointer;
    }

    .enterTodo button:hover{
        background: transparent;
    }
</style>