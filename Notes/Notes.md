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
