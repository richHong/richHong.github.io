---
layout: post
title:  "Google Maps in React"
date:   2016-06-01
categories: javascript
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;So you are working on your React project and you want to integrate Google Maps. That can be a task easier said than done, but with the GMaps NPM package for React and a call to Google's geocode API it can be a rather simple process. This tutorial was made with the expectation that you are using webpack and have that development environment set up. If not, I recommend using the boilerplate found [here](https://github.com/colinlmcdonald/react-redux-webpack). Credit goes to Colin for creating this repository.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The first thing you will need to do is get an API key for google maps. You can get those credential [here](https://console.developers.google.com/) Next, install react-gmaps packages from NPM in your command line.

{% highlight javascript %}
$ npm install react-gmaps
{% endhighlight %}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The next thing you need to do is import your components from the react-gmaps package. We will import the components using curly brackets. The component has four individual components that we can use in our example. The GMaps component is the main component which renders the Google map. The Marker will be nested within the GMaps component to create a marker on the map. The Infowindow creates an info window that can label a location on the map. Circle creates a circle around the location on the map. See the code snippet below.

{% highlight javascript %}
import React, { Component } from 'react';
import { render } from 'react-dom';
import { Gmaps, Marker, InfoWindow, Circle } from 'react-gmaps';

class Map extends Component {
  constructor(){
    super();
    this.state = {location:{
      latitude: null,
      longitude: null
    }};
  }

  onMapCreated(map) {
    map.setOptions({
      disableDefaultUI: true,
      panControl:true,
      zoomControl:true,
      mapTypeControl:true,
      scaleControl:true,
      streetViewControl:true,
      overviewMapControl:true,
      rotateControl:true
    });
  }

  handleSubmit(event, search){
    event.preventDefault();

    fetch('http://maps.googleapis.com/maps/api/geocode/json?address='+search.value)
    .then(response => response.json())
    .then(json => {
      this.setState({location: {
        latitude:json.results[0].geometry.location.lat, 
        longitude: json.results[0].geometry.location.lng}
      });
    });
  }

  componentWillMount() {
    navigator.geolocation.getCurrentPosition(location => {
      this.setState({location: location.coords});
    });
  }

  render(){
    return (
      <div>

        <form onSubmit={event => this.handleSubmit(event, this.search)}>
          <input type='text' ref={input => this.search = input}/>
          <input type='submit'/>
        </form>

        <Gmaps
          width={'900'}
          height={'500'}
          lat={this.state.location.latitude}
          lng={this.state.location.longitude}
          zoom={12}
          loadingMessage={'Be happy'}
          params={{v: '3.exp', key: 'YOUR_API_KEY'}}
          onMapCreated={this.onMapCreated}>
          <Marker
            lat={this.state.location.latitude}
            lng={this.state.location.longitude} />
        </Gmaps>

      </div>
      );
  }
}

render(<Map />, document.getElementById('app'));
{% endhighlight %}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Make sure you enter your API key into the GMaps component. When the page loads, the componentWillMount function will run before the component is mounted or rendered. This piece of code will get your current geolocation from the browser, update the state with that location, and will re-render the map. The form we created will takes in any address and will use fetch to send an API call to Google's geocode API. This will return the longitude and latitude of the searched address and we'll use that result to update our state.. And that's it, you are able to create a dynamic map with a few lines of code.
