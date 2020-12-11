<template>
    <div>
        <form @submit.prevent="addHandler" v-if="!edit">
            <input type="text" v-model="task" />
            <button type="submit">Add</button>
        </form>
        <form @submit.prevent="editHandler" v-if="edit">
            <input type="text" v-model="task" />
            <button type="submit">Edit</button>
        </form>

        <div class="" v-if="tasks && tasks.length > 0">
            <span v-for="(i, task) in tasks" :key="i" class="list">
                {{ tasks[task] }} 
                <div class="task">
                    <button @click.prevent="update(task)" style="width: 5px;">edit</button>
                    <button @click.prevent="destroy(task)" style="width: 5px;">delete</button>
                </div>
            </span>
        </div>
    </div>
</template>

<script>
export default {
    data: () => ({
        task: '',
        tasks: '',
        edit: false,
        editKey: false
    }),
    created (){
        this.fetchTasks()
    },
    methods: {


        clear () {
            this.task = ''
        },


        fetchTasks () {
            this.tasks = JSON.parse(localStorage.getItem('tasks'))
        },


        addHandler () {
            this.tasks = JSON.parse(localStorage.getItem('tasks'))
            if (!this.tasks) {
                const arr = []
                arr.push(this.task)
                localStorage.setItem('tasks', JSON.stringify(arr))
            } else {
                this.tasks.push(this.task)
                localStorage.setItem('tasks', JSON.stringify(this.tasks))
            }
            this.clear()
        },


        editHandler (){
            this.tasks[this.editKey] = this.task
            localStorage.setItem('tasks', JSON.stringify(this.tasks))
            this.clear()
            this.edit = false
        },


        update (key){
            this.edit = true
            this.editKey = key
            this.task = this.tasks[key]
        },


        destroy (key) {
            const arr = this.tasks
            const i = arr.indexOf(key)
            arr.splice(i, key)
            localStorage.setItem('tasks', JSON.stringify(arr))
        }


    }
}
</script>

<style scoped>
.list {
    display: flex;
    flex-direction: column;
    padding: 5px;
}
.task {
    display: flex;
}
</style>