​								**Flutter ImagePicker TroubleShooting**

------

**Concept**

Trouble shooting when using imagepicker

**Method**

In android/build.gradle 

```
subprojects {
    project.configurations.all {
        resolutionStrategy.eachDependency { details ->
            if (details.requested.group == 'com.android.support'
                    && !details.requested.name.contains('multidex') ) {
                details.useVersion "26.1.0"
            }
        }
    }
}
```