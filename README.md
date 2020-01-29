# ReduxReact

**With The SOngs App The reducers will be two reducers, One for Song List and One For Selected Song**
**Will Be A Action Creator of Select Song. The Two Pieces Of State Will Be The Two Reducers In Redux We Change Our State**
**With The Action Creators, An Action Creator Has To Be Caled. It Will Dispatch an Action and tell The Selected Song Reducer**
**To Update Its state to reflect the cureent picked Song, The App is Structured Like This**
**                                 APP                                             **
**                                  |                                              **
**                                  |                       **
**                           _______|______             **
 **                          |            |                        **
**                           |            |                     **
 **                       SONG LIST   SONG DETAIL             **

 **Provider Component Wraps the whole application at the App Level The Connect Component Communictaes with the provider. Both are Created by React-Redux**
 **The Redux Store holds all the Combined Reducers Holding All The State in One Place The Store That Gets created by combining the reducers**
 **Is then passed as a Prop To The Provider Wrapping The APP, Every component That needs to access the data stored in the Redux Store Will get wrapped**
 **With The Connect component from React-Redux The Connect and The Provider Communicates Through the Context System Allowing Any Child Component**
 **To Communicate With Any Parent Component without having to pass props to any child component between them The Connect Component Has To Be Configured**
 **To work with the action creators**

 *Folder Structure*

 **/actions directory contains files related to action creators, /components still has react components, /reducers will hold our reducers**
 **index.js sets up the react and redux sides of the App. The Action Creator needs to return a plain JavaScript Object which is an ACTION.**
 **Redux Actions must have a TYPE property and have an OPTIONAL payload property In This App we Pass in the song we want to select as an argument**
 **To the Action Creator Like So** 

 `export const selectSong = (song) => { `         *This is a Single action creator that returns an action*
 `  return { `
`     type: 'SONG_SELECTED',`
`     payload: song`
`   };`
` };` 

## In our Reducers Directory create a index.js file this will hold both of our reducers
*One will return our static list of songs and one will allow the user to pick a specific song*
**the selectedSongReducer is called with 2 arguments selectedSong defaulted to null and our action object from Above with A SONG_SELECTED type**
**and a payload of the song the user selected**

`const songsReducer = () => {`
`  return [`
 `     {title: 'No Scrubs', duration: '4:05'} `
 `      {title: 'Macarena', duration: '2:30'}`
 `      {title: 'All Star', duration: '3:15'}`
`    ];`
`};`


`const selectedSongReducer = (selectedSong = null, action) => {`
` if (action.type === 'SONG_SELECTED') {`
`   return action.payload;`
` }`

`   return selectedSong;`
`}`

## Combine These Two Reducers To Make the Redux Store

`import { combineReducers } from 'redux';`

`const songsReducer = () => {`
`  return [`
 `     {title: 'No Scrubs', duration: '4:05'} `
 `      {title: 'Macarena', duration: '2:30'}`
 `      {title: 'All Star', duration: '3:15'}`
`    ];`
`};`


`const selectedSongReducer = (selectedSong = null, action) => {`
` if (action.type === 'SONG_SELECTED') {`
`   return action.payload;`
` }`

`   return selectedSong;`
`}`

`export default combineReducers({`        *the keys in this object is the keys that will show up in our state object*
` songs: songsReducer,`
` selectedSong: selectedSongReducer`
`});`

## In The index.js file in the src directory Pass the Provider to the App and the Redux store to the Provider
## We pass the createStore our collection of reducers and it gives us a Redux Store which holds our data or state

`import React from 'react';`
`import ReactDOM from 'react-dom';`
`import { Provider } from 'react-redux';`
`import { createStore } from 'redux';`

`import App from './components/App';`
`import reducers from './reducers/index'`

`ReactDOM.render(`
` <Provider store={createStore(reducers)}>`
`  <App />`
` </Provider>,` 
`document.querySelector('#root')`
`)`

## Now any component can get access to the redux store through the provider with connect, Now in SongList.js

`import React from 'react';`

`class SongList extends React.Component {`
` render() {`
`   return`
` }`
`}`

`export defult SongList;`

## In App.js import the SongList component

`import React from 'react';`
`import SongList from './SongList';`

`const App = () => {`
` return (`
  `<div>`
`   <SongList />`
`  </div>`
`  );`
`}`

## In the SongList component import the connect component

`import React from 'react';`
`import {connect} from 'react-redux';`

`class SongList extends React.Component {`
` render() {`
`   return`
` }`
`}`

`export defult connect()(SongList);`

## Above the connect is basically a function returning a function wraping our SongList which we invoke when wrapping our SongList.
## We Have To Configure The Connect Function with mapStateToProps. mapStateToProps takes our state object all of the data in the redux store
## and we run computations on it to make it show up in our component as props.
## The object we return from the mapStateToProps function will show up as props inside of our component. in The component
## this.props === {songs: state.songs}, this.props holds the list of songs as an Object.

`import React from 'react';`
`import {connect} from 'react-redux';`

`class SongList extends React.Component {`
` render() {`
`   return`
` }`
`}`

`const mapStateToProps = (state) => {`
` return { songs: state.songs }`
`}`

`export defult connect(mapStateToProps)(SongList);`

## To render a list of songs in our SongsList component. Using a helper methos called renderList. we just map over the data provided
## by the redux-store that we created and render the data to the screen.


`import React from 'react';`
`import {connect} from 'react-redux';`

`class SongList extends React.Component {`
`  renderList() {`
`   return this.props.songs.map((song) => {`
`     return (`
`       <div className="item" key={song.title}>`
`         {song.title}`
`       </div>`
`     )`
`   });`
`}`

` render() {`
`   return <div>{this.renderList()}</div>`
` }`
`}`

`const mapStateToProps = (state) => {`
` return { songs: state.songs }`
`}`

`export defult connect(mapStateToProps)(SongList);`