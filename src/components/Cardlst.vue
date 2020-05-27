<template>
    <div class="container">
        <div>
            <div class="card" v-for="archives in data" :key="archives.id">
                <h3> {{archives.date}} : {{archives.time}} </h3>
                <ul v-for="tasks in archives.tasks" :key="tasks.id">
                    <li> {{tasks.id}} - {{tasks.title}} </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name:"Cardlist" ,
  props:['data']
}
</script>


<style scoped>
h3{
    border-bottom: 1px solid gray;
    padding-bottom: 10px;
}
.card{
    background-color :#ffffff;
    width: 50%;
    height: auto;
    border: 1px solid gray;
    border-radius: 10px;
    margin: 10px auto;
}
li{
    list-style: none;
}
</style>
