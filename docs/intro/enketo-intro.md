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

#### Slices and Reducers

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



#### CreateAsyncThunk
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

#### Extra Reducers 

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

#### Actions

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

#### Store

<img src="https://i.postimg.cc/D0DFDmhQ/Screenshot-2023-08-21-202714.png" width="800" height="350" />


##### Redux Store Configuration

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


#### Dispatch
<img src="https://i.postimg.cc/tgv85Jj9/Screenshot-2023-08-21-204222.png" width="800" height="350" />

##### Imports:

- **`fetchUsers`, `setCurrentUser`, `setLoading`, `setUsers` from `@/store/slices/userListSlice`**:
  Actions from the `userListSlice` that are dispatched within the component.

##### `useDispatch` Hook:

- **Purpose**:
  Used to get the `dispatch` method from the Redux store, allowing the component to dispatch actions to the store.

#### Selectors
<img src="https://i.postimg.cc/pLRTNGnp/Screenshot-2023-08-21-204528.png" width="800" height="300" />


The `Home` component retrieves user data from the Redux store using the `useSelector` hook from the `react-redux` library and logs it when it changes.

##### Imports:

- **`useSelector` from `react-redux`**:
  A hook that allows you to extract data from the Redux store state, using a selector function. The hook will also cause your component to re-render when the selected data changes.

##### `useSelector` Hook:

- **Usage**:
  The hook takes a selector function as its argument. This function receives the entire store state and returns the part of the state that this component is interested in.

## Socket IO 🔌