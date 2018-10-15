---
title: "Redux 1"
date: 2018-10-01T21:39:04+05:30
tags : [
    "React",
    "Redux",
    "Interview",
    "Javascript"
   ]
---

## Redux is a predictable state container for JavaScript apps.


```
import { createStore } from "redux"; //an import from the redux library
const store = createStore();  // Takes reducer as argument
```

Store stores the states and reducers handles the communication

Reducers modifies the state based on action in pure state

In redux, all application state exists as a single store object

Spread operator or splat operator copies the contents of one array object into another.


## Steps

- Add a constant to the constants file. Something like `const BLAH = ‘Blah`

- Add an action creator to the actions folder. Return an action JavaScript object with a type of the constant you created.

- Add a reducer to the reducers folder that handles this action creator.



--------

## mapDispatchToProps

In a nutshell, your components are supposed to be concerned only with displaying stuff. The only place they are supposed to get information from is their props.

Therefore, a "well designed" component in the pattern look like this:

```
class FancyAlerter extends Component {
    sendAlert = () => {
        this.props.sendTheAlert()
    }

    render() {
        <div>
          <h1>Today's Fancy Alert is {this.props.fancyInfo}</h1>
          <Button onClick={sendAlert}/>
        </div>
     }
}

```

This component gets the info it displays from props (which came from the redux store via mapStateToProps) and it also gets its action function from its props: sendTheAlert().

That's where mapDispatchToProps comes in: in the corresponding container

```
// FancyButtonContainer.js

function mapDispatchToProps(dispatch) {
    return({
        sendTheAlert: () => {dispatch(ALERT_ACTION)}
    })
}

function mapStateToProps(state} {
    return({fancyInfo: "Fancy this:" + state.currentFunnyString})
}

export const FancyButtonContainer = connect(
    mapStateToProps, mapDispatchToProps)(
    FancyAlerter
)
```

Now that it's the container that knows about redux and dispatch and store and state and ... stuff.

The component in the pattern, FancyAlerter, which does the rendering doesn't need to know about any of that stuff: it gets its method to call at onClick of the button, via its props.

And ... mapDispatchToProps was the useful means that redux provides to let the container easily pass that function into the wrapped component on its props.


(Note: you can't use mapStateToProps for the same purpose as mapDispatchToProps for the basic reason that you don't have access to dispatch inside mapStateToProp. So you couldn't use  mapStateToProps to give the wrapped component a method that uses dispatch.

I don't know why they chose to break it into two mapping functions - it might have been tidier to have  mapToProps(state, dispatch, props) IE one function to do both!


-------

>> Reducers are just pure functions that take the previous state and an action, and return the next state. Remember to return new state objects, instead of mutating the previous state.