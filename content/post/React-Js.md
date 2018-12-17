---
title: "React Hooks"
date: 2018-12-13T22:04:51+05:30
draft: false
tags: [
    "React ",
    "Interview",
    "Javascript"
]
---
# Basics

`Components`  splits the UI into independent, reusable pieces, and think about each piece in isolation.


```

function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// OR


class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}


```

Rendering

```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);

```


-------
## componentDidMount()

Invoked immediately after a component is mounted (inserted into the tree). 

This method is a good place to set up any subscriptions. If you do that, don’t forget to unsubscribe in componentWillUnmount().


You may call setState() immediately in componentDidMount(). It will trigger an extra rendering, but it will happen before the browser updates the screen. This guarantees that even though the render() will be called twice in this case, the user won’t see the intermediate state. 


---
## componentDidUpdate()


An opportunity to operate on the DOM when the component has been updated. 

To do network requests as long as you compare the `current props to previous props` 


```

componentDidUpdate(prevProps) {
  // Typical usage (don't forget to compare props):
  if (this.props.userID !== prevProps.userID) {
    this.fetchData(this.props.userID);
  }
}

```


You may call setState() immediately in componentDidUpdate() but note that it must be wrapped in a condition , or you’ll cause an `infinite loop.`



---
## componentWillUnmount() 

Is invoked immediately before a component is unmounted and destroyed. Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests