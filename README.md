#Spotify API Setup Instructions

https://developer.spotify.com/documentation/general/guides/authorization-guide/

* Git clone Spotify's [account auth example](https://github.com/spotify/web-api-auth-examples) with command
```
git clone https://github.com/spotify/web-api-auth-examples
```
* Follow the installation structions on the readme for that repo.

* Get your api key and secret from the settings page in your [application dashboard](developer.spotifycom/dashboard/applications).

* Plug your application's client_id, client_secret, and redirect_uri (which by default can be 'http://localhost:8888/callback') into lines 15-17 of web-api-auth-examples/authorization_code/app.js. Make sure to set that redirect_uri in your project dashboard settings as well.

* Create a new app (mine is called client) with create-react-app app-name

* In client app, in package.json, in dependencies, add a line for: 
```
spotify-web-api-js":"^0.22.1
```
I suppose for Rails look for a corresponding gem.

* Create a button in your webapp linking to the authentication page:
```
<a href='http://localhost:8888'><Button>Login to Spotify</Button></a>
```

* Add a permission to our authorization scopes. Around line 50, add ' user-read-playback-state' or whatever permissions [Spotify provides](https://developer.spotify.com/documentation/general/guides/scopes/) to the scope.

* Edit the redirect path around line 107 to the client app page:
```
res.redirect('http://localhost:3000/#' +
...
```

* Next we can copy the function getHashParams from web-api-auth-examples/authorization_code/public/index.html line 71 and use it inside the App component in our client app's src/App.js file.

* Use that function by setting its output to a variable.
```
const params = getHashParams()
```

* To display what we're currently playing, add a div for the track name and another for the track image to our App component, making use of params.nowPlaying.name:
```
<div>Now Playing: {params.nowPlaying.name}</div>
<div><img src={params.nowPlaying.image} style={{width:100}}/></div>
```

We'll also set an object in state to track whether our user is logged in or not (don't forget to "import { useState } from 'react'"):
```
const [loggedIn, setLoggedIn] = useState({loggedIn: false})

...
```

* Add a button that will reload what we're listening to.
```
<button onClick={() => getNowPlaying()}>
    Check Now Playing
</button>
```

* Using code from [Spotify's provided helper functions](https://github.com/jmperez/spotify-web-api-js), add:
```
import Spotify from 'spotify-web-api-js'

const spotifyWebAPI = new Spotify()
```
We'll also need to install spotify-web-api-js.
```
npm install spotify-web-api-js -save
```

* Define the function getNowPlaying



* Edit the redirect route around line 50 to ...









## Libraries

[Spotify's Web API Libraries page](https://developer.spotify.com/documentation/web-api/libraries/)

I'm using rails so I'll be using the libraries below.

### Web API Wrappers

Use one of these:
[RSpotify](https://github.com/guilhermesad/rspotify)
    "This is a ruby wrapper for the Spotify Web API."
[spotify-client](https://github.com/icoretech/spotify-client)
    "Ruby Client for the Spotify Web API.

### OAuth2 integration

Ruby omniauth strategy: https://github.com/icoretech/omniauth-spotify
    **Description:** "This gem provides a simple way to authenticate to the Spotify Web API using OmniAuth with OAuth2."
    Add to gemfile:
    ```
    gem 'omniauth-spotify'
    ```

