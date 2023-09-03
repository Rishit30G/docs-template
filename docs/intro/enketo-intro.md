---
title: Developer Experience 🧑🏻‍💻
sidebar_label: Developer Experience 📖
slug: /developer-experience
---

<head>
  <title>Developer Experience 🧑🏻‍💻</title>
  <meta name="description" />
</head>

## Introduction 📖
Welcome, developers! 👋🏻 <br/>
This documentation will provide you with a clear understanding of the project, and we will delve into its core concepts and functionalities. Our goal is to offer you an overview of the project and assist you in getting started. The project is a fusion of various technologies, including React, Redux, NextJS, SocketIO, and ChakraUI, among others. In the following section, we will address all the crucial aspects and functionalities.

## Flow of the Application 🌊 

Here is a diagram to explain the flow of the application: 

![](https://i.postimg.cc/BbZQP7q0/Flowchart.jpg)

### Bot List Retrieval 🤖

#### 1. Initialization
   - Upon loading the application, a request to retrieve all available bots is initiated.
   - If the API call fails, a message "No Bots Found" is displayed to the user.

#### 2. Data Handling with Redux
   - When the bots are successfully retrieved, Redux is used to store the data.
   - With Redux acting as the single source of truth, the application's data integrity is ensured.
   - The `useSelector` hook is employed to fetch and display the bot data within the application.

#### 3. Socket Connection for Bot Interaction
   - When a user selects a specific bot, a socket connection is established using the [socket.io](http://socket.io) library and our custom socket path. This enables a singular channel communication with the bot.
   - Polling is incorporated to handle potential socket connection failures, such as those resulting from poor internet connectivity. Polling consistently checks and re-establishes the connection once the issue is resolved.
   
#### 4. User-Bot Interaction
   - With an established socket connection, the user can interact with bots.
   - Bots are equipped to respond in various formats such as Video, Text, Image, Multiple Choice Questions, etc.
   - Users can "star" specific messages during their conversation. These starred messages are stored in the "Starred Chat" section for future reference.
   - All conversation exchanges are managed via the Redux store, a comprehensive state management solution.

### Starred Messages ⭐

#### 1. Overview
   - The "Starred Messages" section is dedicated to showcasing messages that users have chosen to "star" or bookmark during their conversations with bots.
   
#### 2. Accessing Starred Messages
   - Users can select a particular bot from the list to view all starred messages associated with that bot.

#### 3. Redux Management
   - All functionalities related to starred messages, including saving, retrieving, and displaying, are managed using Redux and the specific slices designed for this purpose.

## Redux Toolkit 🧰
[Redux Toolkit](https://redux-toolkit.js.org/) stands as a purposeful toolkit designed by the Redux team to streamline and enhance Redux development. It sets a preferred approach for crafting Redux logic and governing state within your JavaScript applications, serving as the endorsed method for these tasks. 

### Slices and Reducers 🍰

<img src="https://i.postimg.cc/B6fTJzwK/Screenshot-2023-08-21-192705.png" width="400" height="450" />

##### Slices
- **users (Array)**: A list of users. Each user can be any object or data structure, depending on what's passed in through the setUsers action.
- **currentUser (Object)**: Represents the currently selected or active user. Its structure depends on what's passed in through the setCurrentUser action.
- **loading (Boolean)**: A flag to indicate whether a certain process or request related to this slice of state is currently ongoing.
- **error (String)**: If there's an error while processing any user-related tasks, this field will store the error message or description.

##### Reducers

- **setUsers**<br/>
**Payload**: Array of users<br/>
**Behavior**: Sets the `users` state to the provided array of users from the payload.

- **setCurrentUser** <br/>
**Payload**: User object<br/>
**Behavior**: Sets the `currentUser` state to the provided user object from the payload.

- **setLoading**<br/>
**Payload**: Boolean value<br/>
**Behavior**: Sets the `loading` state to the provided boolean value from the payload.

- **setError**<br/>
**Payload**: String value representing an error message.<br/>
**Behavior**: Sets the `error` state to the provided string value from the payload.



### CreateAsyncThunk 🎁

<img src="https://i.postimg.cc/13DgSrbg/Screenshot-2023-08-21-195235.png" width="800" height="400" />

##### `fetchUsers` Function
This function fetchs user (bot list) data from a specified API endpoint.

**Type** <br/>
Asynchronous Thunk Action creator provided by the Redux Toolkit's `createAsyncThunk` method.

**Return** <br/>
A Promise that resolves to the data fetched from the API.

**Usage**<br/>
This function can be dispatched using Redux's `dispatch` method to initiate the API call. The result will be automatically handled by Redux Toolkit, setting the state according to the lifecycle of the request (pending, fulfilled, rejected).

**Implementation Details**
- **Endpoint URL**: Uses the `axios.get` method to request data from the API endpoint specified in the environment variable `NEXT_PUBLIC_UCI_BASE_URL`. Defaults to an empty string if the variable isn't defined.
- **Data Retrieval**: Retrieves the data using the `response.data` attribute.
- **Error Handling**: While not explicitly shown in this function, if there's an error during the API call, `createAsyncThunk` will automatically dispatch a rejected action.

### Extra Reducers 🦾 

<img src="https://i.postimg.cc/jS5Dwngc/Screenshot-2023-08-21-200905.png" width="800" height="400" />

##### `extraReducers` in Redux Slice

`extraReducers` provides a way to handle actions defined outside of the slice or to handle async thunk actions. The provided configuration handles actions generated by the `fetchUsers` async thunk.

##### Cases:

###### `fetchUsers.pending`:

- **Purpose**: Handle the state when the `fetchUsers` request is initiated and is still in progress.
- **State Changes**:
  - `state.loading`: Set to `true`. Indicates that the fetch operation is currently loading.

###### `fetchUsers.fulfilled`:

- **Purpose**: Handle the state when the `fetchUsers` request is successfully completed.
- **State Changes**:
  - `state.loading`: Set to `false`. The fetch operation has completed.
  - `state.users`: Updated with the data fetched from the API, provided in `action.payload`.

###### `fetchUsers.rejected`:

- **Purpose**: Handle the state when the `fetchUsers` request fails for any reason.
- **State Changes**:
  - `state.loading`: Set to `false`. The fetch operation has ended.
  - `state.error`: 
    - If there's an error message available in `action.error.message`, it will be saved to this attribute.
    - If not, it defaults to `'Unknown Error Occured'`.

### Actions 🤾🏻‍♀️

<img src="https://i.postimg.cc/QCFXNcxK/Screenshot-2023-08-21-201728.png" width="1000" height="180" />

##### `userListSlice` Export and Actions Destructuring

The provided code segment pertains to the exports from a Redux slice, specifically the `userListSlice`.

##### `export { userListSlice }`:

- **Purpose**: 
  Exports the entire `userListSlice` object. This includes the reducer and all actions generated by the slice.
  
##### `export const { setUsers, setCurrentUser, setLoading, setError } = userListSlice.actions`:

- **Purpose**: 
  Destructures and exports specific actions from the `userListSlice`. 

- **setUsers**: 
  An action to set or update the users list in the state.

- **setCurrentUser**: 
  An action to set or update the current selected/active user in the state.

- **setLoading**: 
  An action to toggle the loading state, typically used to indicate whether data fetching or some asynchronous operation is in progress.

- **setError**: 
  An action to set or update an error message in the state, typically used when an error occurs during an operation.

### Store 🏬

<img src="https://i.postimg.cc/D0DFDmhQ/Screenshot-2023-08-21-202714.png" width="800" height="350" />


#### Redux Store Configuration

The given code sets up a Redux store using Redux Toolkit's `configureStore` function, integrating reducers from different slices and incorporating logging via the `redux-logger` middleware.

##### Imports:

- **`configureStore` from `@reduxjs/toolkit`**: 
  Function to easily configure a Redux store with some best-practice defaults.

- **`userListSlice` from `./slices/userListSlice`**: 
  Redux slice pertaining to the user list data and actions.

- **`userMessagesSlice` from `./slices/userMessageSlice`**: 
  Redux slice concerning user messages data and actions.

- **`logger` from `redux-logger`**: 
  Middleware to log actions and state changes in the Redux store.

##### Store Configuration:

- **`export const store`**: 
  The main Redux store for the application.

##### Reducers:

The `reducer` object combines two slices:

- **`userList`:** 
  Refers to the reducer from the `userListSlice`. Manages state related to users.

- **`userMessages`:** 
  Refers to the reducer from the `userMessagesSlice`. Manages state related to user messages.

##### Middleware:

Middleware has been enhanced to include the `redux-logger`. This ensures that every Redux action and subsequent state change gets logged in the console.

- **`getDefaultMiddleware().concat(logger)`**: 
  This gets the default set of middleware from Redux Toolkit and adds (`concat`) the `redux-logger` middleware to it.

##### Additional Types:

- **`export type AppDispatch`**: 
  A type definition for the dispatch method of the store. It can be used in the application to type the dispatch method when dispatching actions, especially useful with TypeScript.


### Dispatch 📮

<img src="https://i.postimg.cc/tgv85Jj9/Screenshot-2023-08-21-204222.png" width="800" height="350" />

##### Imports:

- **`fetchUsers`, `setCurrentUser`, `setLoading`, `setUsers` from `@/store/slices/userListSlice`**:
  Actions from the `userListSlice` that are dispatched within the component.

##### `useDispatch` Hook:

- **Purpose**:
  Used to get the `dispatch` method from the Redux store, allowing the component to dispatch actions to the store.

### Selectors 🎯

<img src="https://i.postimg.cc/pLRTNGnp/Screenshot-2023-08-21-204528.png" width="800" height="300" />


The `Home` component retrieves user data from the Redux store using the `useSelector` hook from the `react-redux` library and logs it when it changes.

##### Imports:

- **`useSelector` from `react-redux`**:
  A hook that allows you to extract data from the Redux store state, using a selector function. The hook will also cause your component to re-render when the selected data changes.

##### `useSelector` Hook:

- **Usage**:
  The hook takes a selector function as its argument. This function receives the entire store state and returns the part of the state that this component is interested in.

### sendMessage Slice 📩

![](https://i.postimg.cc/sgcBQLnb/Screenshot-2023-09-03-140458.png)

- The userMessages Redux slice manages state related to user messages within the application. Created using Redux Toolkit's createSlice function, it streamlines the state and reducers into a single, coherent module.

The initial state for the userMessages slice comprises:

- `messages`: A list of all user messages.
- `activeUserMessage`: Represents the currently highlighted or viewed user message.
- `loading`: Indicates whether a specific operation related to messages is ongoing.
- `error`: Captures any potential errors during message operations.
- `starMessage`: Holds messages that have been marked as significant or starred.

Reducers dictate how the state evolves in response to dispatched actions. For the userMessages slice, the following reducers are available:

- `setMessages`: Updates the list of messages.
- `setActiveUserMessage`: Alters the active user message.
- `setStarMessage`: Updates the list of starred messages.
- `setLoading`: Adjusts the loading status.
- `setError`: Modifies the error state.

Each reducer is accompanied by a respective action which can be dispatched to enact its intended changes on the state.


## Socket IO 🔌

![](https://i.postimg.cc/vm1QJBbp/Screenshot-2023-08-25-080902.png)

### SocketConnection Component 🧩

#### Overview

The `SocketConnection` component is a functional React component responsible for establishing and configuring a socket connection. The component provides the necessary setup options for the socket and establishes the connection when certain conditions are met.

#### Props
##### isMobileAvailable

- **Type:** `boolean`
- **Description:** Indicates if the mobile device is available.

##### setSocket

- **Type:** `Function`
- **Description:** Callback function to set the socket. Not utilized in the provided code snippet, might be needed for other use-cases.

##### setNewSocket

- **Type:** `Function`
- **Description:** Callback function to establish a new socket connection.

##### onMessageReceived

- **Type:** `Function`
- **Description:** Callback function to be invoked when a message is received from the socket.

##### newSocket

- **Type:** `Object`
- **Description:** Represents the new socket instance, if available.

#### Internals

##### options

The component uses the `useMemo` hook to memoize the socket connection options. These options include:

- `socketOptions`: Configuration related to the socket connection.
  - `polling.extraHeaders`: Headers to be sent with the polling request.
  - `query`: The device ID, retrieved from local storage, is sent as a query with the connection.
  - `autoConnect`: Indicates whether the socket should automatically connect upon creation.
  - `upgrade`: Indicates whether the transport should upgrade from long-polling to something better.
- `onRecieveCallback`: Callback function to handle received messages.

##### useEffect

The `useEffect` hook is responsible for:

1. Reading the socket URL from the environment variables.
2. If the `newSocket` is not established, it will utilize the `setNewSocket` function to establish a new connection using the options provided.

##### Return

This component does not render any UI elements, hence it returns `null`.

### Socket Event Handlers 🤝🏻

![](https://i.postimg.cc/PrbC6jZz/Screenshot-2023-08-25-083139.png)

#### Overview

The provided code snippet defines a series of event handlers and a callback for managing socket interactions and processing messages. The events include connecting, disconnecting, receiving a bot response, encountering exceptions, and establishing a session. The primary goal of these handlers is to manage socket states, display potential error messages, process incoming messages, and update the message state accordingly.

#### Event Handlers

#### `onConnect`

- **Signature:** `function onConnect(): void`
- **Description:** This handler is triggered when the socket establishes a successful connection. It sets the connection state to `true`.

#### `onDisconnect`

- **Signature:** `function onDisconnect(): void`
- **Description:** Triggered when the socket disconnects. It sets the connection state to `false`.

#### `onException`

- **Signature:** `function onException(exception: any)`
- **Description:** This handler captures any exceptions or errors thrown during the socket interactions. It then displays the exception message using a toast notification.

#### `onSessionCreated`

- **Signature:** `function onSessionCreated(sessionArg: { session: any })`
- **Description:** Triggered when a new session is created with the socket. It sets the new session data to the component's state.

#### Message Processing Callback

#### `onMessageReceived`

- **Signature:** `const onMessageReceived = useCallback((msg: SocketResponse): void => {...}, [messages, updateMsgState])`
- **Description:** This callback is responsible for:
  - Parsing and determining the message type (e.g., IMAGE, AUDIO, VIDEO, DOCUMENT, FILE, TEXT).
  - Updating the message state with relevant details, including the message's content and any associated media URLs.
  - Storing the processed message into local storage.

#### Socket Event Bindings

If a socket instance exists and isn't currently connected, the code binds the aforementioned event handlers to the relevant socket events. This ensures that when an event occurs on the socket, the appropriate action or state update is triggered.

### Socket Package 📦 

Here is a breief documentation for socket package used in the project. Full documentation can be found [here](https://www.npmjs.com/package/socket-package).

![](https://i.postimg.cc/QtSnSN5z/Screenshot-2023-08-25-085128.png)

#### Overview

The `UCI` class provides a structured way to interact with a socket using the `socket.io-client`. The main responsibilities of the class include establishing a socket connection, handling messages, managing the socket session, and sending messages.

###### `socket`

- **Type:** `Socket | undefined`
- **Description:** Represents the socket instance, initially undefined.

###### `msgReceiveCb`

- **Type:** `Function`
- **Description:** Callback function to handle received messages.

###### `session`

- **Type:** `any`
- **Description:** Represents the current session of the socket. 

#### Constructor

- **Signature:** `constructor(URL: string, socketOptions: any, onRecieveCallback: any)`
  - `URL`: The URL for establishing the socket connection.
  - `socketOptions`: Configuration options for the socket.
  - `onRecieveCallback`: Callback function to handle received messages.
  
The constructor initializes and connects to a socket, sets the message receive callback, and binds the handlers for "botResponse" and "session" events.

#### Methods

###### `handleMessage`

- **Signature:** `handleMessage(message: any): void`
- **Description:** Logs the received message to the console and invokes the message receive callback.

##### `handleSocketSession`

- **Signature:** `handleSocketSession(session: any): void`
- **Description:** Sets the received session data to the class's `session` property.

##### `onDisconnect`

- **Signature:** `onDisconnect(): void`
- **Description:** Disconnects the socket if connected.

##### `sendMessage`

- **Signature:** `sendMessage({ text, to, from, optional }: any): void`
  - `text`: Message content.
  - `to`: The recipient of the message.
  - `from`: The sender of the message.
  - `optional`: An object containing optional parameters such as `appId`, `channel`.

---

Hope the documentation was helpful and you got good insights on how things are streamlining and working in the project! 📖 <br/>
Make sure to share it with your friends and colleagues, who are looking forward to contributing to the project and exponentially grow their learning curve 🚀 <br/>
Don't forget to explore official [Sunbird UCI](https://uci.sunbird.org/) page and [UCI Github Repository](https://github.com/samagra-comms/uci-web-channel) 🙌🏻
