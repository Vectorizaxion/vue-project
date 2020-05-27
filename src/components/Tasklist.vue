<template> <!--HTML Structure -->
    <div class="container">
        <div class="task-zone">

            <div class="drop-zone" @drop="onDrop($event,'todo')" @dragenter.prevent @dragover.prevent> <!-- Todo object-->
                <h1> TO-DO </h1>
                <div class="drag-el" draggable @dragstart="onStart($event,task)" v-for="task in todoList" :key="task.id">{{task.title}}</div> <!--Item A-->
            </div>

            <div class="drop-zone" @drop="onDrop($event,'doing')" @dragenter.prevent @dragover.prevent > <!--Doing object-->
                <h1> Doing </h1>
                <div class="drag-el" draggable @dragstart="onStart($event,task)"  v-for="task in doingList" :key="task.id">{{task.title}}</div> <!--Item B-->
            </div>

            <div class="drop-zone" @drop="onDrop($event,'done')" @dragenter.prevent @dragover.prevent >  <!-- Doing object-->
                <h1> Done </h1>
                <div class="drag-el" draggable @dragstart="onStart($event,task)" v-for="task in doneList" :key="task.id">{{task.title}}</div> <!--Item C-->
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
            ]
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
</style>