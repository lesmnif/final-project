<template>
  <div class="space-y-6">
    <div class="bg-white px-4 py-5 shadow sm:rounded-lg sm:p-6">
      <div class="md:grid md:grid-cols-2 md:gap-6">
        <div class="md:col-span-1">
          <h3 class="text-lg font-medium leading-6 text-gray-900">Add New Task</h3>
          <p class="text-red-500">{{errorMsg}}</p>
        </div>
        <div class="mt-5 space-y-6 md:col-span-2 md:mt-0">
          <div class="grid grid-cols-3 gap-6">
            <div class="col-span-3 sm:col-span-2">
              <label
                class="block text-sm font-medium text-gray-700"
                >Title</label
              >
              <div class="mt-1 flex rounded-md shadow-sm border-black">
                <input
                  v-model="title"
                  type="text"
                  class="block w-full flex-1 rounded-md border border-gray-400 focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm"
                />
              </div>
            </div>
          </div>

          <div>
            <label for="about" class="block text-sm font-medium text-gray-700"
              >Description</label
            >
            <div class="mt-1">
              <textarea
                v-model="description"
                rows="2"
                class="block w-full rounded-md border border-gray-400 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm"
              />
            </div>
          </div>
          <div class="flex justify-end">
            <button
              @click="addTask()"
              class="ml-3 inline-flex justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
            >
              Save
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "@vue/reactivity";
import { useTaskStore } from "../stores/task";

const emit = defineEmits(["handleClick"])

function addTask(){
  if(title.value.length < 4){
    errorMsg.value = "Title must be at least 4 characters"
 
    return setTimeout(() => {
      return errorMsg.value = null
    },2000)
  }
  emit("handleClick", title.value, description.value)
  title.value=""
  description.value=""
}

const title = ref("")
const description = ref("")
const errorMsg = ref(null)

const handleClick = async () => {

  await useTaskStore().addTask(title.value, description.value)
  await useTaskStore().fetchTasks()
}

// constant to save a variable that define the custom event that will be emitted to the homeView

// constant to save a variable that holds the value of the title input field of the new task

// constant to save a variable that holds the value of the description input field of the new task

// constant to save a variable that holds an initial false boolean value for the errorMessage container that is conditionally displayed depending if the input field is empty

// const constant to save a variable that holds the value of the error message

// arrow function to call the form holding the task title and task description that uses a conditional to first checks if the task title is empty, if true the error message is displayed through the errorMessage container and sets a timeOut method that hides the error after some time. Else, its emmits a custom event to the home view with the task title and task description; clears the task title and task description input fields.
</script>

<style></style>
