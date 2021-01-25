---
layout: post
title:      "React Router"
date:       2021-01-25 18:29:28 +0000
permalink:  react_router
---




Thanks to Rauter, SPAs - single-page applications looks like multiple pages to user. By cliking on link or entering a URL, SPA can render  components like separate pages.
React comes without routing. First we need to install library named react-router with:  npm install react-router-dom or yarn add react-router-dom.  Also we need to import BrouserRouter, Route, Switch and Link from 'react-router-dom';
If we need routing in our entire app, we must wrap our higher component with BrowserRouter, so we need to wrap App component.  In index.js: 

```
// index.js

import React, { Component } from 'react';
import App from './App'
import { BrowserRouter as Router } from 'react-router-dom'

ReactDOM.render(
    <BrowserRouter>
        <App />
    </BrowserRouter>, 
    document.getElementById('root')
)

```

In App component, we need to add the Switch element. These ensure that only one component is rendered at a time. Also we need to add  <Route> tags. These are the links between the components and should be placed inside the <Switch> tags. 
To tell the <Route> tags which component to load :
* 	add a path attribute - the path of the route (for home page is path="/") 
* 	component attribute with the name of the component we want to load  (component={Home})
* 	exect before path - to make sure that path is going to match exactly what is written in path string 

```
//App.js

import React, { Component } from 'react';
import { Route, Switch } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';
import NavBar from './components/NavBar

function App() {
    return (
        <div fluid className="App">
	           <NavBar>
             <Switch>
                    <Route exact path="/" component={Home} />
                    <Route exact path="/about" component={About} />
              </Switch>
        </div >
    )
}

```

With Route in App.js, site is only navigable by typing the URLs. To add clickable links to the site, we use the Link element from React Router in a new  component Navbar that we should import in App.js. Instead of using a tag and href, React Router uses Link and  to="/…" to be able to switch between pages without reloading it.

```
//NavBar.js

import { Link } from 'react-router-dom';

function Navbar() {
  return (
    <div>
      <Link to="/">Home </Link>
      <Link to="/about">About Us </Link>
    </div>
  );
};

```



