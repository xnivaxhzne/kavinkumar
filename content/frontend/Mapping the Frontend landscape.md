I wanted to put together a map of frontend technologies to show how I think about the ecosystem and where different tools fit. 

But before diving into frameworks, libraries, and tools, it's worth stepping back. Frontend isn't just about code. Every choice we make as engineers sits inside a tension between four different forces:

1. End User - App should feel fast, simple and accessible
2. Developer - Code should be easy to build, scale and maintain
3. Business - Feature should reach market quickly at lower cost
4. Browser - Enforces limits on what can be rendered

To define UIs, we need languages that express our intentions. On frontend, the essential ones are:
1. HTML - to give structure
2. CSS - to style
3. Javascript - to add interactivity

A common addition is Typescript, which makes you to write a bit more code but in return it catches bugs early and improves developer experience like autocompletion, in-code documentation. In the end, Typescript gets complied to Javascript since the browser only understands HTML, CSS, and JavaScript. Any other language is just for developer convenience. 

Technically, every modern frontend application can be built entirely with those three core languages without any frameworks. But in practice, that's hard to build, scale, and maintain. Why? Because you'd need to write way more lines of code, enforce structure manually, and spend energy on boilerplate instead of solving real business problems. Building only with HTML, CSS, JS is like building a skyscraper with just bricks and cement, while modern tools give you cranes, blueprints and prefabs.

The starting point for modern frontend development is usually picking a framework or a library. At first glance they seem the same, but they're not. A library gives you pieces of the puzzle, you call it when you need it. A framework gives you the whole puzzle box with rules included, it calls your code, not the other way around. For example, React is a library. It only handles rendering the UI. If you need routing, forms, or state management, you bring in extra libraries. Angular, on the other hand, is a full framework. It comes with built-in solutions for routing, forms, HTTP calls, and more.

One core thing every frontend app deals with is data. The UI is just a reflection of stored data shown to the user, and in turn it collects user input and sends it back after some manipulation or validation. Different businesses have different data needs, but the pattern is the same: data flows **to the user** and **from the user**. The channel for this is usually **APIs**.

Data doesn't flow as some arbitrary stream, it flows as named entities. From the API level itself, you're dealing with things like `users`, `posts`, `products`, `orders`.

The simplest flow looks like this:
- When a route is visited, fetch data.
- Display it to the user.
- When the route changes, discard it.
- If the user visits again, fetch fresh data.

This is the lowest effort path: less code, but the user might wait on every navigation for new API calls. 
The other approach is: write more code to make it smooth. Fetch once, then keep it around. On the next visit, load from cache instead of hitting the server again. This is where state management come into play.

The same trade-off shows up when you update data.
- Simple path: just send the update to the server and wait for a response before updating the UI.
- Better UX path: instantly update the UI first, and then sync with the server. This technique is called optimistic updates.
So again, less code vs smoother UX.

A more advanced pattern is introducing a store.
- The store holds a local copy of your data.
- It stays in sync with the database by updating, invalidating, or merging data.
- Your rendering layer doesn't talk directly to APIs anymore, it talks to the store.
- The store becomes the single source of truth, and the UI just reacts to changes.

This way, you get a smoother UX and a cleaner separation of concerns, but you also write more code and take on more complexity.