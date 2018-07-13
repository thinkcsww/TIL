**Android shared preferences**

------



**First make a SharefPrefs Class in Utilities folder**



```
class SharedPrefs(context: Context) {
    val PREFS_FILENAME = "prefs"
    val prefs: SharedPreferences = context.getSharedPreferences(PREFS_FILENAME, 0)

    val IS_LOGGED_IN = "isLoggedIn"
    val AUTH_TOKEN = "authToken"
    val USER_EMAIL = "userEmail"

    var isLoggedIn: Boolean
        get() = prefs.getBoolean(IS_LOGGED_IN, false)
        set(value) = prefs.edit().putBoolean(IS_LOGGED_IN, value).apply()

    var authToken: String
        get() = prefs.getString(AUTH_TOKEN, "")
        set(value) = prefs.edit().putString(AUTH_TOKEN, value).apply()

    var userEmail: String
        get() = prefs.getString(USER_EMAIL, "")
        set(value) = prefs.edit().putString(USER_EMAIL, value).apply()

    var requestQueue = Volley.newRequestQueue(context)
}
```

Gettter and setter automatically save values in the sharedpreferences.

All i need to do is using like this.

```
App.prefs.userEmail = response.getString("user")
                App.prefs.authToken = response.getString("token")
                App.prefs.isLoggedIn = true
```



**Second make a App class in Controller folder**



Extends Application and using companion object to make it global

```
class App : Application(){

    companion object {
        lateinit var prefs: SharedPrefs
    }
    override fun onCreate() {

        prefs = SharedPrefs(applicationContext)
        super.onCreate()
    }
}
```



**How to use**



1. Get = App.prefs.isLoggedIn -> just call variable than it will work
2. Set = App.prefs.isLoggedIn = true -> just assign value than it will work