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