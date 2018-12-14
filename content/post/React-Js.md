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