# Vue JS

## Getting Started with Vue JS

- Vue JS is a frontend framework which is much more light weight than any other framework in the market now.
- Vue JS is know for its simplicity and since it is light weight, its known for performance and since it follows the same concepts of having components in it, hence its scalability.
- One thing that seperates Vue from React is that it is `injectable`.

### Using Vue without installing it (CDN).

- We can use Vue as usual by `npm install` ing it but we can also use Vue without installing it. We can just `inject` it into our html file using it's `CDN`. The CDN link must be added in the `head` of the HTML.
- Now Vue JS is already injected via the CND, to use it, we just simply need to create a variable in the `script.js` file and assign a object.
- Inside the object, first we need to write a `data` method. Here, we always have to return something, usually it'll be an object consisting of variables and methods.
- After doing the above, since we're injecting Vue via cdn, we'll have access to a method called `Vue.createApp` inside where we'll inject the above variable.
- Then we need to mount it somewhere to utilize everything inside it, for that, we can chain a `mount()` where we can pass a class or id.

  ```js
  const App = {
    data() {
      return {
        name: "Hello, World",
      };
    },
  };

  Vue.createApp(App).mount("#app");
  ```

- The point is we can inject Vue by just targeting any class or id by just using Vue CDN and it works.
  ```js
  // one more way of injecting Vue, in the same script.js file of above example.
  Vue.createApp({
    data() {
      return {
        name: "Hello, Vue JS!",
      };
    },
  }).mount("#oneMoreApp");
  ```
- Here, even though we're using same variable name - `name` in the above, yet there's no conflict. This is because, when we're using `Vue.createApp`, it's creating completely different app, hence there's no conflict.

## Basics of Vue JS

#### Data Binding

- One of the core advantages of Vue is not just able to target a particular div but actually propagate some of the data from our script file to the actual HTML element.
- To bind the data, we'll use double flower brackets just like in angular.

  ```html
  <h1>{{ someVariableName }}</h1>
  ```

#### Directives

- Directives are used to inject variable values in HTML attributes. There are two kinds in Vue, they are `:` and `@`. These are the shorthand notation of some of the directives given to us by Vue JS.
  ```html
  <img :src="someVariableName" />
  ```
- There's something called `V-bind` which is responsible for binding the HTML elements with the script variables that we're passing on. There are different kinds of bindings. We can find more about it [here](https://vuejs.org/api/built-in-directives.html).
- The `@` directives are mainly used for binding events.

#### Handling arrays

- We use `v-for` directive for looping.
- Whenever there's a directive on an element, we don't want to put another directive inside it except in case of looping. To increase the performance, we use `:key` directive.
  ```html
  <div class="col-md-12 vapp">
    <div
      class="card mt-3"
      style="width: 18rem"
      v-for="course in courseList"
      :key="course.id"
    >
      <img
        :src="course.courseImage"
        class="card-img-top"
        :alt="course.courseName"
      />
      <div class="card-body">
        <h5 class="card-title text-dark">{{course.courseName}}</h5>
        <p class="card-text text-dark">{{course.subtitle}}</p>
        <a href="#" class="btn btn-primary">Rs. {{course.price}}</a>
      </div>
    </div>
  </div>
  ```

#### Handling conditionals and booleans

- Vue gives us special directive known as template aka `<templete></template>` for conditional rendering. It doesn't show in the view, it just disappears after rendering the elements inside it.
- For conditional rendering, we use `v-if` and `v-else` and they need to be next to one another else if there's any element between, it won't work.

  ```js
  // in script.js file
  const App = {
    data() {
      return {
        isLogin: true,
        anotherBool: true,
      };
    },
  };

  Vue.createApp(App).mount(".vapp");
  ```

  ```html
  <!-- in html file -->
  <template v-if="!isLogin">
    <li class="nav-item">
      <a class="nav-link" href="#">Sign Up</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Sign In</a>
    </li>
  </template>
  <template v-else>
    <li class="nav-item">
      <a class="nav-link" href="#">Logout</a>
    </li>
  </template>
  ```

- There's a similar directive to `v-else` known as `v-show`. It doesn't actually remove the element from rendering into your HTML entirely but rather it makes the element's `display: none;`.
- Hence, most of the developers avoid `v-show` as using `v-else` gives more performance (rendering wise).

## 2 way binding in Vue JS

- To bind the data, there's a special directive given to us by Vue called `v-model`.

  ```html
  <!-- in html -->
  <input type="text" v-model="someVariableName" />
  ```

  ```js
  // in script.js file
  const App = {
    data(){
      return {
        someVariableName = '';
      }
    }
  }

  Vue.createApp(App).mount('#vapp');
  ```

- Here when we use `v-model`, the value of the input is automatically stored in the variable passed in the `v-model` directive.

#### Computed and methods in VueJS

- If we want to write functions inside a Vue app, then we write it inside a property called `methods`.
- There's also this thing inside the Vue app called `computed`. Inside this also we can have methods.
- The one foundational difference between the two is that we `cannot` pass on `parameters` to the methods inside `computed` whereas we `can` pass on `parameters` to the methods inside `methods`.

  ```js
  const App = {
    data(){
      return {...}
    },
    methods: {
      someFunc1(param?) {...}
    },
    computed: {
      myFunc1() {...}
    }
  }
  ```

- Other difference is that, we can write the methods inside `methods` too instead of inside `computed` but whenever the data changes, the methods inside `computed` automatically runs can stays upto date with the data where as the methods inside `methods` won't, we have to manually call them.
- To use computed method, just use the method's name like a variable.
  ```html
  <h1>{{ myFunc1 }}</h1>
  ```

### Lifecycle Hooks in VueJS

- Refer the Vue documentation.

## Vue CLI and GUI

- First install Vue CLI using the following command.
  ```
  npm install -g @vue/cli
  ```
- Then, we need to install Vue using the following command.
  ```
  npm install vue@next
  ```
- Now, to create new Vue project, we can use the following command.
  ```
  vue create project_name
  ```
- We can also create projects using Vue GUI and to access it, we can use the following command.
  ```
  vue ui
  ```

### Vue file structure breakdown

- In Public folder, there's `index.html` which consists of an empty div with `#app`. All the Vue components are mounted onto this div #app.
- Majority of the time, we'll be spending our time in `src` folder. Inside it we have `main.js` which does createApp() and injects `App.vue` and mounts it to the `#app` in `index.html`.
- `App.vue` is where we write our code, here the basic structure is:
  - template element - where we write the HTML.
  - script element - where we write the JS.
  - style element - where we wtite the CSS.

## Conditionals in VueJS

- We can use directives like `v-if`, `v-if-else`, and `v-else` to conditionally show or not show a componenet or an HTML element.

## Components and third party libraries

- In the modern world of React, Angular or Vue, `component` is the foundation of building different web sites or web frameworks or whatever you're designing.
- To include third party libraries, use can include them in the `main.js` file and make use of `.use` to include them as shown below.

  ```js
  import VueSweetalert2 from "vue-sweetalert2";
  import "sweetalert2/dist/sweetalert2.min.css";

  const app = creatApp(App);
  app.use(VueSweetalert2);
  app.mount("#app");
  ```

- Whenever we're adding any component, we'll have to include in the export default of `App.vue` using the `components` property.
  ```js
  components: {
    Icon;
  }
  ```
- `Props` - To have a prop, we should have a `props` property. It can be an array or object. At the time of calling the component, one can pass the prop.
  ```js
  export default {
    props: {
      iconName: {
        type: String, // makes sure only string is passed.
        required: true, // makes sure props are required when the component is used.
      },
    },
  };
  ```
- `Watcher` - It was added in Vue3 and we can put a watcher on a variable or array and if that thing changes, it'll notify you. Once we get the notification, we can run a method or something like that.
- Using the property `watch`, inside we can give any variables to keep a watch on.
- The watcher function's parameter get's the changed variable content which can be accessed using that variable name.
  ```js
  watch: {
    someVariable: function(msg){
      if(msg){
        // call method to display popup
      }
    }
  }
  ```

## Handling localstorage in VueJS

- `Form` - One of the good things of forms in Vue is that - You don't have to say inside your script `preventDefault()`. Instead, we can add `@submit.prevent` attribute on the form itself as well as we can also provide name of the method which should run when the form submits.
  ```html
  <form @submit.prevent="onSubmit"></form>
  ```
- To do something when the component first mounts, we can use a lifecycle hook called `mounted()`. Here we can check if there's something in localStorage and grab it.
  ```js
  export default {
    name: 'App',
    data(){...},
    methods: {...},
    mounted() {
      const data = JSON.parse(localStorage.getItem("@movies"));
      if (data) {
        try {
          this.movies = data;
        } catch (e) {
          localStorage.removeItem("@movies");
        }
      }
    },
  };
  ```

## Handling API's in VueJS

- Handling API's in Vue is similar to how we handle API's in vanilla JavaScript.
- To make things easier, we can use `axios` for requesting API's.
- We just need to install `axios`, then import it and can start using it.
  ```js
  import axios from "axios";
  ```
- We can use axios with `.then and .catch` block or we can use it along with `async and await`.
  ```js
  export default {
    name: "App",
    methods: {
      fetchUser: async function () {
        try {
          const res = await axios.get("https://randomuser.me/api/");
          this.user = res.data.results[0];
        } catch (e) {
          console.error(e);
        }
      },
    },
    mounted() {
      this.fetchUser();
    },
  };
  ```
- We can use a lifecycle method `mounted()` to call the api when the component is first mounted.

## Routing and State Management in VueJS

#### Routing

- While creating the app, when asked to select a preset, we need to choose `Manual select features` and select `Router` for adding routing to the app, and select `Vuex` if you want to add `state management` to the app.
- Next, hit `yes` when asked for `use history mode for router`.
- Next choose everything default options till the app is created except for config file where we choose `package.json`.
- If we see the `main.js`, you can find something like this.
  ```js
  createApp(App).use(router).mount("#app");
  ```
- This means router has been injected as middleware and throught this middleware, the router keyword as going to be available anywhere in the app.
- `Middleware` - Let's say you have a single web page and on that you have login page and this same page is used by both admin and user. Middleware helps in determining who is admin and user by providing additional functionality `in-between` whatever we want to do. Hence the name middleware.
- We also notice `router-link` being used in `App.vue`. These are almost similar to links i.e `a href`.

  ```html
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>

    <!-- different ways of navigating to a page -->

    <router-link :to="path: '/account'">Account</router-link>

    <!-- using query params -->
    <router-link :to="{path: `/account/${course.id}`, query: {token: 'abc'}}"
      >Account</router-link
    >
    <router-link :to="`/account/${course.id}`">Account</router-link>
  </nav>
  ```

- As seen from the above, there are different ways of navigating to a page.
- The actual routes are declared inside the `router` folder inside `index.js`.

  ```js
  const routes = [
    {
      path: "/",
      name: "home",
      component: HomeView,
    },
    {
      path: "/about",
      name: "about",
      // route level code-splitting
      // this generates a separate chunk (about.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () =>
        import(/* webpackChunkName: "about" */ "../views/AboutView.vue"),
    },
    {
      path: "/account/:id",
      name: "account",
      component: Account,
    },
  ];
  ```

- To access the query params, we can use route or router with $ sign prepended to it.

  ```html
  <h1>{{ $route.params.id }}</h1>

  we can also access it using router

  <h1>{{ $router }}</h1>
  ```

#### State Management

- When we include `Vuex`, there'll be extra folder called `store` which contains a `index.js` file. This is where all variables are stored, hence referred to as single source of truth.
