<template>
    <div>
        <h1>
            Task list!
        </h1>
        <button @click="handleShowList"> Show list!</button>
        <br>
        <input 
            type="text" 
            v-focus 
            v-model="currentTask"
            @keyup.enter="handleAddTask"
        >
        <ul v-if="showList">
            <li 
                v-for="(task, index) in tasks"
                :key="`${task}-${index}`"
                @dblclick="complete(task)"
                class="task-item"
                :class="{'line-through' : task.isDone}"
            >
                {{task.name}}
                <button @click="remove(task)">&times;</button>
            </li>
        </ul>
        <p v-else>Hidden tasks</p>
    </div>
</template>

<script>
    function handleShowList(){
        this.showList = !this.showList
    }

    function handleAddTask(){
        this.tasks.push({
            name: this.currentTask,
            isDone: false
        })
        this.currentTask = ''
    }

    function remove(task){
        this.tasks = this.tasks.filter(t => t.name !== task.name)
    }

    function complete(task) {
        this.tasks = this.tasks.map(t => {
            if (t.name === task.name) {
                return {...t, isDone: !t.isDone}
            } else {
                return {...t}
            }
        })
    }

    const focus = {
        inserted: (el) => {
            el.focus()
        }
    }

    export default {
        directives: {
            focus
        },
        data: () => ({
            showList: false,
            currentTask: '',
            tasks: [
                {name: 'Do it!', isDone: false},
                {name: 'Do it again!', isDone: false}
            ]
        }),
        methods: {
            complete,
            remove,
            handleShowList,
            handleAddTask
        }
    }
</script>

<style scoped>
    .line-through {
        text-decoration: line-through;
    }
    .task-item {
        cursor: pointer;
    }
</style>