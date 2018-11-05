​								Flutter Widget Callback

------

**Concept**

Do something after widget is build completely

**Method**

Put this function inside the Widget 

```
WidgetsBinding.instance.addPostFrameCallback((_) {

//Do Something

);
    });
```

