​									  **Publishing Android app**

------



**Concept**

Publising android app on google play store

1. Removing log  -> pro guard

```
buildTypes {
        release {
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
```

Inside the proguard rule 

```
-assumenosideeffects class android.util.Log {
    public static boolean isLoggable(java.lang.String, int);
    public static int v(...);
    public static int i(...);
    public static int w(...);
    public static int d(...);
    public static int e(...);
}
```

2. Check the error report from here 

`[app module]/build/reports/lint-results-yourBuildName-fatal.html`.

