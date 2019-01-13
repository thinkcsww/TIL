​										**Redux**

------



created a store -> where our state lives!

we cannot make a store without a reducer!

a reducer is a function that determines what our state looks like and how we change the state1 



0 - create a reducer with some initial state

1 - create a store -> the reducer is run and our initial state is defined

2 - whenever we want to see our state -> store.getState()

3 - whenever we want to make a change to our state -> store.dispatch()

4 - actions are objects

5 - actions must have a key of type

6 - writing a function that returns an object

7 - write a function that returns an action



**Data flow**

1.  rootReducer -> return new redux state -> mapToProps -> Render 

