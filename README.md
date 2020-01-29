# Redux

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