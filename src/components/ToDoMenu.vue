<script setup>
    import ToDoTask from './ToDoTask.vue';
    import { ref } from 'vue';

    const taskName = ref("")
    const toDoList = ref([])

    function addToDo(taskName){
        if(taskName) {
            let task = {
                name: taskName,
                complete: false
            }
            toDoList.value.push(task);
        } else {
            alert('Introduce un nombre para la tarea.');
        }
    }

    function deleteToDo(index){
        toDoList.value.splice(index,1)
    }

    function changeCheckValue(index) {
        if(!toDoList.value[index].complete) {
            toDoList.value[index].complete = true;
        } else {
            toDoList.value[index].complete = false;
        }
    }

    function deleteComplete() {
        toDoList.value.forEach((value, index) => {
            if(toDoList.value[index].complete) {
                toDoList.value.splice(index)
            }
        });
    }

    function deleteAll() {
        toDoList.value.splice(0)
    }

    function toComplete() {
        return toDoList.value.filter(task => !task.complete).length;
    }

</script>

<template>
    <div id="todo" class="container">
        <header class="row align-items-center">
            <h2 class="col-12">Lista de Tareas</h2>
        </header>
        <div id="addTask" class="row justify-content-center">
            <input placeholder="Introduzca el nombre de la tarea..." maxlength="65" v-model="taskName" type="text" class="col-8"></input>
            <button type="submit" class="col-1" @click="addToDo(taskName)"><i class="bi bi-clipboard2-plus-fill"></i></button>
        </div>
        <div id="list">
            <div v-if="!toDoList.length" id="complete">
                <h2>¡Sin tareas!</h2>
                <i class="bi bi-check-circle-fill"></i>
            </div>
            <ToDoTask v-else v-for="(task, index) in toDoList" :name="task.name" @delete="deleteToDo(index)" @changeCheck="changeCheckValue(index)"/>
        </div>
        <div id="control" class="row justify-content-evenly">
            <button class="col-4" @click="deleteComplete()">Limpiar completados</button>
            <button class="col-4" @click="deleteAll()">Borrar rodo</button>
        </div>
        <div id="ntask" class="row">
            <span class="col-12">Tareas por completar: {{ toComplete() }}</span>
        </div>
    </div>
</template>

<style scoped>
    #todo{
        margin-top: 2%;
        width: 60%;
        border-radius: 10px 10px 0px 0px;

        header {
            background-color: rgba(0, 110, 255, 0.548);
            border-radius: 10px 10px 0px 0px;

            h2 {
            text-align: center;
            font-weight: bold;
            color: white;
            }
        }
    }

    #addTask{
        background-color: rgba(0, 110, 255, 0.548);
        padding-bottom: 15px;

        input[type="text"] {
            padding-right: 50px;
            border-radius: 5px;
            border: 1px solid rgba(24, 135, 163, 0.651);
        }

        input[type="text"]:focus  {
            outline: none;
        }

        button {
            margin-left: -8%;
            border-radius: 0px 5px 5px 0px;
            background: rgb(0, 102, 255);
            color: white;
            border: 0;
        }
    }

    #list{
        border-left: 1px solid rgba(24, 135, 163, 0.651);
        border-right: 1px solid rgba(24, 135, 163, 0.651);
        #complete{
            text-align: center;

            h2 {
                font-weight: bolder;
            }

            i {
                color: green;
                font-size: 60px;
            }
        }
    }

    #control{
        background-color: rgba(0, 110, 255, 0.548);
        padding: 10px 0px 10px 0px;

        button {
            background-color: white;
            border: 1px solid black;
            border-radius: 5px;
        }

        button:hover {
            border: 1px solid gray;
        }
    }

    #ntask{
        background-color: rgba(0, 110, 255, 0.548);
        padding: 10px 0px 10px 0px;
        border-radius: 0px 0px 10px 10px;
        color: white;
        font-weight: bold;
    }
</style>