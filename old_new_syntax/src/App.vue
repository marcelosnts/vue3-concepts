<template>
    <div>
        <h1>
            Tasks list!
        </h1>
        <button @click="handleShowList"> Show list!</button>
        <br>
        <input 
            type="text" 
            v-focus 
            v-model="state.currentTask"
            @keyup.enter="handleAddTask"
        >
        <ul v-if="state.showList">
            <li 
                v-for="(task, index) in state.tasks"
                :key="`${task}-${index}`"
                @dblclick="handleComplete(task)"
                class="task-item"
                :class="{'line-through' : task.isDone}"
            >
                {{task.name}}
                <button @click="handleRemove(task)">&times;</button>
            </li>
        </ul>
        <p v-else>Hidden tasks</p>
    </div>
</template>

<script>
    import { reactive } from 'vue'

    const focus = {
        inserted: (el) => {
            el.focus()
        }
    }

    export default {
        directives: {
            focus
        },
        setup () {
            const state = reactive({
                showList: false,
                currentTask: '',
                tasks: [
                    {name: 'Do it!', isDone: false},
                    {name: 'Do it again!', isDone: false}
                ]
            })

            function handleShowList(){
                state.showList = !state.showList
            }

            function handleAddTask(){
                state.tasks.push({
                    name: state.currentTask,
                    isDone: false
                })
                state.currentTask = ''
            }

            function handleRemove(task){
                state.tasks = state.tasks.filter(t => t.name !== task.name)
            }

            function handleComplete(task) {
                state.tasks = state.tasks.map(t => {
                    if (t.name === task.name) {
                        return {...t, isDone: !t.isDone}
                    } else {
                        return {...t}
                    }
                })
            }

            return {
                state,
                handleShowList,
                handleAddTask,
                handleRemove,
                handleComplete
            }
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