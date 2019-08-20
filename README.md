## Aim:

The aim of this exercise is to use Vue.js. It requires that you write a single page app that retrieves data from the API. When the app loads, it should retrieve the list of users from API and display them. Clicking on the name of the user should display 10 recent posts written by that user. Clicking on the title of the post displays the details of the post.

## API URLs:

    Users: https://jsonplaceholder.typicode.com/users

    Posts: https://jsonplaceholder.typicode.com/posts

## Prerequisites

* [Install npm](https://nodejs.org/en/)

## Steps

### 1. Create a new repository `blogging`
### 2. Use Sourcetree to clone this repo
### 3. Initialize the project

[Create a project using cli](https://cli.vuejs.org/guide/creating-a-project.html#vue-create)
```console
npm install vue
vue create .
```
[Create a project using GUI]
```console
vue ui
```

Compile and hot-reload for development, See [Configuration Reference] for more commands(https://cli.vuejs.org/config/).
```console
npm run serve
```

Visit http://localhost:8080/

### 5. [Install Element](https://element.eleme.io/#/en-US/component/installation#npm)

```console
npm i element-ui -S
```

### 6. [Import Element](https://element.eleme.io/#/en-US/component/quickstart#import-element)

### 7. Write code of Drawer with fake data

To focus on how drawer works

### 8. Use [axios](https://github.com/axios/axios) to fetch data over HTTP

[Using Axios to Consume APIs](https://vuejs.org/v2/cookbook/using-axios-to-consume-apis.html)

```console
npm install axios
```

./src/components/BlogManager.vue
```javascript
import axios from 'axios';

  ...
  methods: {
    fetchUsers() {
      axios
        .get("https://jsonplaceholder.typicode.com/users")
        .then(response => (this.users = response.data));
    },
    ...
````

### 8. Get user list when the app loads

```javascript
  mounted() {
    this.fetchUsers();
  }
```

### 9. Get selected user

```html
<el-table :data="users" border stripe @row-click="onUserSelected">
```

```javascript
    onUserSelected(row) {
      console.log(row.id);
      console.log(row.name);
      console.log(row.email);
    }
````

### 10. Fetch posts which are written by the selected user

```javascript
    fetchPostsWrittenBySelectedUser(selectedUser) {
      axios
        .get("https://jsonplaceholder.typicode.com/posts")
        .then(
          response =>
            (this.postsWrittenBySelectedUser = response.data.filter(
              x => x.userId === selectedUser.id
            ))
        );
    },
```

## Challenges

### 1. Layout & the drawer view

#### Progress:
Google components of nested drawer for vue.js

#### Solution:

[Element UI](https://element.eleme.io/#/en-US/component/drawer#nested-drawer)

### 2. Filter an array by a given value

#### Solution:
Stackoverflow

## Things to do

### 1. CoreUI
### 2. Unit test
### 3. Subcomponent
### 4. E2e Test (Selenium)
