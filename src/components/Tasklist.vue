<template> <!--HTML Structure -->
    <div class="container">
        <div class="add-task">
            <input id="new-task" type="text" v-model="newTask">
            <button type="button" @click="addTask(newTask)">Add New Task </button>
        </div>
        <div class="task-zone">

            <div class="drop-zone" @drop="onDrop($event,'todo')" @dragenter.prevent @dragover.prevent> <!-- Todo object-->
                <h1> TO-DO </h1>
                <div class="drag-el" draggable @dragstart="onStart($event,task)" v-for="task in todoList" :key="task.id">
                    <span v-if="editTask != task.id">{{task.title}}</span>
                    <input v-else class="edit-task" type="text" v-model="task.title">

                    <button v-if="editTask != task.id"  type="button" @click="onEdit(task)"> Edit </button>
                    <button v-else type="button" @click="EditedTask(task)"> Save </button>

                    <button type="button" @click="deleteTask(task)"> Delete </button>
                </div> 
            </div>

            <div class="drop-zone" @drop="onDrop($event,'doing')" @dragenter.prevent @dragover.prevent > <!--Doing object-->
                <h1> Doing </h1>
                <div class="drag-el" draggable @dragstart="onStart($event,task)"  v-for="task in doingList" :key="task.id">
                     <span v-if="editTask != task.id">{{task.title}}</span>
                    <input v-else class="edit-task" type="text" v-model="task.title">
                    
                    <button v-if="editTask != task.id"  type="button" @click="onEdit(task)"> Edit </button>
                    <button v-else type="button" @click="EditedTask(task)"> Save </button>

                    <button type="button" @click="deleteTask(task)"> Delete </button>
                </div> <!--Item B-->
            </div>

            <div class="drop-zone" @drop="onDrop($event,'done')" @dragenter.prevent @dragover.prevent >  <!-- Doing object-->
                <h1> Done </h1>
                <div class="drag-el" draggable @dragstart="onStart($event,task)" v-for="task in doneList" :key="task.id">
                     <span v-if="editTask != task.id">{{task.title}}</span>
                    <input v-else class="edit-task" type="text" v-model="task.title">

                    <button v-if="editTask != task.id"  type="button" @click="onEdit(task)"> Edit </button>
                    <button v-else type="button" @click="EditedTask(task)"> Save </button>

                    <button type="button" @click="deleteTask(task)"> Delete </button>
                </div> <!--Item C-->
            </div>

        </div>
    </div>
</template>

<script> //JS Strcture
export default {
    name : 'Tasklist',
    data(){ //Item List
        return{
            task:[
                {
                    id:1,
                    title:'Item A',
                    status:'todo'
                },
                {
                    id:2,
                    title:'Item B',
                    status:'todo'
                },
                {
                    id:3,
                    title:'Item C',
                    status:'todo'
                },
                {
                    id:4,
                    title:'Item D',
                    status:'doing'
                },
                {
                    id:5,
                    title:'Item E',
                    status:'done'
                },
            ],
            newTask : "",
            editTask : ""
        }
    },
    computed:{ //Filler Status
        todoList(){
            return this.task.filter(task => task.status == 'todo')
        },
        doingList(){
            return this.task.filter(task => task.status == 'doing')
        },
        doneList(){
             return this.task.filter(task => task.status == 'done')
        }
    },
    methods:{
        onStart(e,task){
            e.dataTransfer.dropEffect = "move"
            e.dataTransfer.effectAllowed ="move"
            e.dataTransfer.setData('taskID', task.id)
        },
        onDrop(e,newstatus){
            const taskId = e.dataTransfer.getData('taskID')
            const task = this.task.find(task => task.id == taskId)
            task.status = newstatus
        },
        addTask(newTask){
            let newID = this.task.length + 1
            this.task.push({id:newID,title:newTask,status:'todo'})
            this.newTask = ""
        },
        onEdit(task){
            this.editTask = task.id
        },
        EditedTask(editnewtask){
            const task = this.task.find(task => task.id == editnewtask.id )
            task.title = editnewtask.title
            this.editTask = ""
        },
        deleteTask(deleteTask){
            this.task = this.task.filter(task => task.id != deleteTask.id)
        }
    }
}
</script>

<style scoped> /* CSS Stucture */
.container{
    margin: 30px;
}
.task-zone{
    display: flex;
    justify-content: space-around;
}
.drop-zone{
    border: 1px solid black;
    width: 250px;
    height: 400px;
    padding: 10px 0;
}
.drag-el{
    border: 1px solid black;
    width: 200px;
    height: 40px;
    margin: 5px auto;
    padding-top: 15px; 
}
.add-task{
    margin: 30px 0;
}
</style>