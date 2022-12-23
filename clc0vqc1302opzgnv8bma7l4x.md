# The importance of React-query and why you should use it

React-query is a powerful tool for managing and fetching data in your React applications. It allows you to quickly bring, cache, and update data from APIs. It also helps you avoid the common pitfalls of working with async data in a declarative framework like React.

One of the main benefits of react-query is its ability to automatically manage the loading state of your data. When a query is in flight, react-query automatically sets the **isLoading** flag to **true**. When the data arrives, it will put it to **false**. This can be extremely useful when you have multiple queries that need to be displayed in a single component, as you can avoid the complexity of manually tracking the loading state of each individual query.

## Caching
Another benefit of react-query is its ability to **cache** and **deduplicate** data. When using react-query, you can specify a cache policy for each query, determining how long the data should be stored before being **refetched**. This can be especially useful when working with APIs with a rate limit, as you can avoid unnecessary requests and ensure that your data is always fresh without overloading the API.

_Here's an example of how you might use react-query in a simple React component_:

```js
import { useQuery } from 'react-query'

function MyComponent() {
  const { data, isLoading } = useQuery('todos', () =>
    fetch('https://my-api.com/todos').then(res => res.json())
  )

  if (isLoading) {
    return <p>Loading...</p>
  }

  return (
    <ul>
      {data.map(todo => (
        <li key={todo.id}>{todo.text}</li>
      ))}
    </ul>
  )
}
```
In this example, we use the **useQuery** hook to fetch a list of todos from an API. While the data is being fetched, the **isLoading** flag is **true**, and the component will display a loading message. Once the data arrives, it will be rendered in a list.

## Query dependencies
React-query also provides a way to optimize the data fetching process using a concept called "query dependencies." Query dependencies are variables that, when changed, will trigger a refetch of the data. This can be especially useful when you have multiple related queries, as it allows you to avoid unnecessary refetches when only one query has changed.

For example, consider a scenario where you have a search form that allows the user to filter a list of products by category and price range. Without query dependencies, you might be tempted to create two separate queries for the category and price range filters like this:
```js
const { data: categoryData } = useQuery(['categories', categoryId], () =>
  fetch(`https://my-api.com/categories/${categoryId}`).then(res => res.json())
)

const { data: priceRangeData } = useQuery(['priceRanges', priceRangeId], () =>
  fetch(`https://my-api.com/priceRanges/${priceRangeId}`).then(res => res.json())
)
```
However, this approach has several drawbacks. For one, it requires you to make two separate requests to the API, which can be inefficient if the data is largely overlapping. It can also be challenging to track which data belongs to which query, especially if you have multiple queries in a single component.

To solve these problems, you can use query dependencies to create a single query responsible for fetching the category and price range data. To do this, you can pass an array of query dependencies as the second argument to the **useQuery** hook:
```js
const { data } = useQuery(
  ['products', categoryId, priceRangeId],
  () =>
    fetch(
      `https://my-api.com/products?categoryId=${categoryId}&priceRangeId=${priceRangeId}`
    ).then(res => res.json()),
  {
    queryFn: (key, queryFn) =>
      queryFn().then(data => {
        return {
          data,
          // We can use the query dependencies to store the category and price range data
          // separately from the products data
          category: categoryData,
          priceRange: priceRangeData
        }
      }),
    enabled: categoryId && priceRangeId // Only fetch if both categoryId and priceRangeId are present
  }
)
```
With this approach, the **useQuery** hook will only refetch the data when either the **categoryId** or **priceRangeId** variables change. This allows you to avoid unnecessary refetches, and keep your data organized in a single, easy-to-manage object.

## Refetch
One of the most powerful features of react-query is the ability to manually trigger a **refetch** of data using the refetch function. This can be especially useful when you need to provide your users with the ability to refresh the data on demand or when you need to update the data in response to a user action.

To use the **refetch** function, you can pass it as a prop to your component using the **useQuery** hook:
```js
const { data, isLoading, refetch } = useQuery('todos', () =>
  fetch('https://my-api.com/todos').then(res => res.json())
)

function handleRefreshClick() {
  refetch()
}

return (
  <>
    {isLoading ? (
      <p>Loading...</p>
    ) : (
      <ul>
        {data.map(todo => (
          <li key={todo.id}>{todo.text}</li>
        ))}
      </ul>
    )}
    <button onClick={handleRefreshClick}>Refresh</button>
  </>
)
```
In this example, we use the **refetch** function in the **handleRefreshClick** event handler, which is triggered when the user clicks the "Refresh" button. When the button is clicked, the **refetch** function is called, starting a new fetch of the data and updating the component with the latest data.

You can also pass options to the **refetch** function to customize how the data is fetched. For example, you can give an object with a **throwOnError** property to specify whether the function should throw an error if the fetch fails:
```js
function handleRefreshClick() {
  refetch({ throwOnError: true }).catch(error => {
    console.error(error)
  })
}
```
In this example, the **refetch** function will throw an error if the fetch fails, which allows you to handle the error in a catch block. This can be especially useful when you need to display an error message to the user or when you need to perform some other action in response to the error.

## Invalidate
In addition to the **refetch** function, react-query also provides several other functions that can help you manage the data in your React components. One such function is the invalidate function, which allows you to **invalidate** the data in the cache and trigger a refetch of the data.

The **invalidate** function can be beneficial when you need to force a refetch of the data, regardless of whether the data is stale or not. For example, consider a scenario where you have a "log out" button in your application that needs to clear the cache and refetch the data when the user logs out. To do this, you can use the **invalidate** function like this:
```js
const { data, isLoading, invalidate } = useQuery('todos', () =>
  fetch('https://my-api.com/todos').then(res => res.json())
)

function handleLogout() {
  invalidate()
}

return (
  <>
    {isLoading ? (
      <p>Loading...</p>
    ) : (
      <ul>
        {data.map(todo => (
          <li key={todo.id}>{todo.text}</li>
        ))}
      </ul>
    )}
    <button onClick={handleLogout}>Log Out</button>
  </>
)
```
In this example, we use the **invalidate** function in the **handleLogout** event handler, which is triggered when the user clicks the "Log Out" button. When the button is clicked, the **invalidate** function is called, which will clear the cache and trigger a new fetch of the data.

You can also pass options to the **invalidate** function to customize how the data is invalidated. For example, you can give an object with a **hard** property to specify whether the data should be invalidated from the cache immediately or whether it should be allowed to expire naturally before being removed:
```js
function handleLogout() {
  invalidate({ hard: true })
}
```
In this example, the **invalidate** function will immediately remove the data from the cache and trigger a refetch, regardless of whether the data is stale or not. This can be especially useful when you need to ensure that the data is refreshed as soon as possible.

---

In summary, react-query is a powerful tool that can greatly simplify the process of working with async data in your React applications. Whether you're building a simple to-do list or a complex real-time dashboard, react-query can help you easily fetch, cache, and update data from APIs, and manage the loading state of your data in a declarative way.

if you're interested to know more about the react-query, you can check it out at
[https://tanstack.com/query/v4/docs/react/overview](https://tanstack.com/query/v4/docs/react/overview)