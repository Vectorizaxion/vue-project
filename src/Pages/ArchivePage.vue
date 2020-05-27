<template>
    <Cardlist :data = "archives"></Cardlist>
</template>

<script>
import Cardlist from '../components/Cardlst.vue'
export default {
    name: 'ArchivePage',
    components : {
        Cardlist
    },
    data(){
        return{
            archives:[
                {
                    date:"20-02-2020",
                    time : "10.00",
                    task:[
                        {   id:1,title:"Item 1",status:"done"},
                        {   id:2,title:"Item 2",status:"done"}
                    ]
                },
                {
                    date:"21-02-2020",
                    time : "10.00",
                    task:[
                        {   id:1,title:"Item 1",status:"done"},
                        {   id:2,title:"Item 2",status:"done"}
                    ]
                }
            ]
        }
    }
}
</script>