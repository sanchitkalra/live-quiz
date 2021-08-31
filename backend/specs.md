# Websocket Server Specification

## Requests

1. Authorisation request
    ```
    {
        "request-type": 1, // authorisation request
        "timestamp": new Date(), // the timestamp at which the client sent the request
        "game-id": "" // 6 character alpha-numeric gme ID
    }
    ```
    
    returns
    ```
    {
        "auth-token": "", // a unique alpha-numeric string to identify the user
        "timestamp": "" // timestamp of when the token was generated
    }
    ```

2. Registration request
    ```
    {
        "request-type": 2 // registration request
        "auth-token": "", // the provided auth-token when user is connected to a game
        "user-name": "" // the user chooses a public display name for games 
    }
    ```
    
    returns
    ```
    {
        "user-name": "", // the same public display name is returned by the server
    }
    ```
    
3. Question response request
    ```
    {
        "request-type": 3, // respond to a question
        "auth-token": "",
        "question-id": "", // unique alphanumeric question ID
        "answer-id": "", // unique alphanumeric answer ID
        "timestamp": new Date() // timestamp at which the question was answered
    }
    ```
    
    returns
    ```
    {
        "accepted": 1, // if the solution was accepted or rejected
        "correct-ans-id": "" // alphanumeric id of the correct answer
    }
    ```
    
## Broadcasts

1. Question broadcast
    ```
    {
        "broadcast-type": 1, // the server is broadcasting a new question
        "question-id": "", // alphanumeric ID
        "question-statement": "",
        "options": [
            {
                "option-id": "", // alphanumeric ID
                "option-text": ""
            } // such 4 items
        ],
        "last": 0 // 0 or 1 depending if it is the last question, 0 - false, 1 - true
    }
    ```
    
2. Leaderboard broadcast
    ```
    {
        "broadcast-type": 2, // the server is broadcasting the leaderboard
        "leaderboard": [ 
            {
                "user-name": "", // the public display name of the user
                "score": 3562 // an integer value representing the score of the user
            }
        ] // array of the results object, pre-sorted
    }
    ```
    This broadcast only happens after the last question has been answered by all eligible users.