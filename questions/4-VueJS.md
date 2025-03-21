# Vue.js Questions & Answers

## Question:
- Explain Vue.js reactivity and common issues when tracking changes.
- Describe data flow between components in a Vue.js app
- List the most common cause of memory leaks in Vue.js apps and how they can be solved.
- What have you used for state management
- What’s the difference between pre-rendering and server side rendering?


## Answer:

### 1. Explain Vue.js reactivity and common issues when tracking changes.
Vue.js uses a reactive data-binding system, where data is "reactive." This means that when data changes, the DOM (or view) updates automatically to reflect those changes. Vue achieves this by using getters and setters on each reactive property, so it can track changes and trigger re-renders when necessary.

#### Common Issue :
- Non-reactive properties: If you add new properties to an object or array that Vue is not aware of, it may not trigger a re-render. For example:
    ```js
    this.someObject.newProperty = 'new'; // Vue won’t react to this change
    ```
    Solution: Use Vue.set to ensure reactivity:
    ```js
    this.$set(this.someObject, 'newProperty', 'new');
    ```
- Array mutation issues: Some array methods like push or splice are reactive, but methods like sort, reverse, or directly setting an index may not trigger reactivity as expected.
    ```js
    this.someArray[0] = 'newValue';  // Might not trigger reactivity
    this.$set(this.someArray, 0, 'newValue');  // Correct way
    ```

### 2. Describe data flow between components in a Vue.js app.
In Vue.js, data flow typically happens in a unidirectional manner. The flow can be summarized as follows:
- Parent to Child (Props): The parent component can pass data to child components via props.
    ```js
    <template>
        <ChildComponent :message="parentMessage" />
    </template>

    <script>
        export default {
            data() {
                return {
                    parentMessage: 'Hello from parent!'
                };
            }
        }
    </script>
    ```
- Child to Parent (Events): Children can communicate with parents using custom events.
    ```js
    <!-- Parent Component -->
    <ChildComponent @childEvent="handleChildEvent" />

    <!-- Child Component -->
    <template>
        <button @click="sendToParent">Click me!</button>
    </template>
    <script>
        export default {
            methods: {
                sendToParent() {
                    this.$emit('childEvent', 'Data from child');
                }
            }
        }
    </script>
    ```
- Global State (Vuex): For shared state between components, Vuex can be used for state management.

### 3. List the most common cause of memory leaks in Vue.js apps and how they can be solved.
- Event Listeners: Forgetting to remove event listeners can cause leaks. Solution: Use this.$off to remove custom event listeners in the beforeDestroy hook.
    ```js
    mounted() {
        this.$on('customEvent', this.handleCustomEvent);
    },
    beforeDestroy() {
        this.$off('customEvent', this.handleCustomEvent);
    }
    ```
- Unused Component Instances: If a component is removed from the DOM but not properly destroyed, it might leave memory usage high. Solution: Always ensure to clean up when components are destroyed, particularly for components with subscriptions or external integrations.

### 4. What have you used for state management?
I've worked extensively with Vuex for state management. Vuex is the official state management library for Vue.js that provides a centralized store to manage the state of an application. With Vuex, you can use state, mutations, actions, and getters to manage and manipulate application data across components.

Example :
```js
// store.js
export const store = new Vuex.Store({
  state: {
    counter: 0
  },
  mutations: {
    increment(state) {
      state.counter++;
    }
  },
  actions: {
    incrementAsync({ commit }) {
      setTimeout(() => {
        commit('increment');
      }, 1000);
    }
  },
  getters: {
    getCounter(state) {
      return state.counter;
    }
  }
});
```

### 5. What’s the difference between pre-rendering and server-side rendering?
- Pre-rendering: This is a technique where the HTML is generated at build time, which means pages are rendered into static HTML files. This is typically used for static websites or sites with content that doesn’t change often. Example: In Vue, you can use vue-cli-plugin-prerender to pre-render your app at build time.

- Server-Side Rendering (SSR): In SSR, the HTML is generated on the server for each request, which means that the server sends fully rendered HTML to the client. This allows for dynamic content and faster initial page load compared to client-side rendering (CSR). Example: With Vue.js, SSR can be achieved using Nuxt.js, which provides a framework for building SSR applications with Vue.

    #### Differences:
    - Pre-rendering generates static HTML at build time.
    - SSR generates dynamic HTML on the server at runtime.