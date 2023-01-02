# GID - To Do App

Welcome to GID ! GID allows you to create, view, and complete tasks on your to do list.

GID is an application running on Vue 3 with the composition API, Pinia as a state management tool, vue router, vite and lastly Supabase running on the backend.

You can use this project as an advanced starter template for something similar, ready to plug in your supabase variables and run directly on a local server already connected to your Supabase instance.

## Features

- Create tasks with his corresponding description
- View a list of all tasks, including their status (in progress or complete)
- Mark tasks as complete
- Edit the description and due date of a task
- Delete the tasks
- Log in feature with Confirmation Mail.

## Environment Variables

To run this project, you will need to change the following environment variables to your .env file with the corresponding values from your Supabase project itself.

`VITE_SUPABASE_URL`

`VITE_SUPABASE_ANON_KEY`

If you have any trouble check out the following Supabase Guide on how to get a project started with Vue 3:

[Supabase Getting Started Vue 3](https://supabase.com/docs/guides/getting-started/tutorials/with-vue-3)

## Run Locally

Clone the project

```bash
  git clone https://github.com/lesmnif/todo-gid.git
```

Go to the project directory

```bash
  cd todo-gid
```

Install dependencies

```bash
  npm install
```

Start the server

```bash
  npm run start
```

## Demo

https://gid-todo.vercel.app/
