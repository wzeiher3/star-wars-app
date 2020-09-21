



<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/wzeiher3/repo">
    <img src="images/ierabbit.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">Star Wars React App - With Hooks!</h3>

  <p align="center">
    Simple API search App using hook-based React components.
    <br />
    <a href="https://github.com/wzeiher3/star-wars-app.git">
      <strong>Explore the docs »</strong>
    </a>
    <br />
    <br />
    <a href="https://star-wars-app-black.vercel.app/">"Vercel" Demo</a>
    ·
    <a href="https://github.com/wzeiher3/star-wars-app.git/issues">Report Bug</a>
    ·
    <a href="https://github.com/wzeiher3/star-wars-app.git/issues">Request Feature</a>
  </p>
</p>

<!-- About The Project -->
---
# Star Wars App
### No class components?! Hooks and Custom Hooks, oh my!
---

## A quick overview on the Hooks...
#### 1. useState()
> ---
>* Since functional components can't construct state like class-based components, we can use the 'useState' hook in the following format:
> ```
> const [state, setState] = useState()
> ```
> ...or to be more terse...
> ```
> const [variableName, updateMethod()] = useState(initialValue)
> ```
>* You can then use the "set" method to "set" the value somewhere in your component
> ```
> <button onClick={setState('I got clicked')} />
> ```
> ---

#### 2. useEffect()
> ---
>* Since functional components can't use lifecycle methods like class-based components, we can use the 'useEffect' hook in the following format:
> ```
> useEffect(() => {
>  // some code here...
> }, [dependencies])
> ```
>* useEffect() will always run on initial render of the component (think componentDidMount() ) and be ran again if the depencies change within the component (think of it as a listener to trigger componentDidUpdate() )
> ---

#### 3. useCallback()
> ---
>* In the use-case of my custom hook "use-GetData" (I won't get into creating custom hooks here, but basically it's just offloading logic outside the component), the useCallback() hook acts as a wrapper for an asynchronous function: and API fetch. Hooks inherently cannot be async functions, so must be wrapped in a useCallback(). In this case, I combine both useEffect() and useCallback(), using the effect hook as a listener to activate the callback:
> ```
>useEffect(() => {
>    if (data === '') return; // no data? nothing happens
>    getTheData()             // data? call the function
>  }, [data])   // listens for change in data
> ```
>* Now that the listener is in place, we can declare a callback to run an asynchronous API fetch:
> ```
>const getTheData = useCallback(() => {
>  async function fetchData() {  // declare async function inside callback
>    const theData = await fetch(url)
>    ...
>    setResults("fetchData")     // useState hook
> ```
>* With the custom hook's state now updated, you can return any pertinent data back to where the hook was called. This makes custom hooks very powerful, as they can be called and used from any component in the app to run logic where needed (though in this case I only need in once):
> ```
>// import { useGetData } from './customHooks/use-GetData'
>const App = () => {
>  const [search, setSearch] = useState('')
>  const { results, ...otherData } = useGetData(search) // asign returned data to variables
>  ...
>  const handleFormSubmit = (formData) => {
>    setSearch(formData) /* this changes data passed to useGetData(),
>  ...                      triggering the listener in it's useEffect() */
>  ...
>  // use "results" to render app and/or child components
> ```
> ---

*These are very basic use cases for hooks, and there are many other rules and quirks not mentioned here, along with many other **types** of hooks. For more info...*

<p align="center">
  <a align="center" href="https://github.com/wzeiher3/star-wars-app.git">
    <strong>Checkout the React docs!!! »</strong>
  </a>
</p>

---
## Sass and Fluid Element Sizing:
1. For the **@mixin "fluid-type"**, I've adapted code written by **Indrek Paas https://gist.github.com/indrekpaas** he's got some other very clever Sass stuff as well.
2. For the loading icon, I adapted **this codepen https://codepen.io/alanshortis/pen/eJLVXr?editors=1100** with minor adjustments to fit the needs of this app
3. Obviously, minimal styling was used here. Mainly, this build was a study on functional skills, less so on graphical techniques
