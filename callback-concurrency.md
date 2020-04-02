# callback concurrency

So I found myself doing android things, and there, unlike javascript async/await, concurrency is achieved throught callbacks

I found the interesting case where I had to map a future (change it's type). Let's see.

# future mapping

Let's say there is this Kotlin function

```kotlin
fun getJson(url: Url, jsonCallback: (Json) -> Unit): Unit = {}
```

that is, a function that lets you subscribe (through callback) to a json

and this function

```kotlin
fun toUser(json: Json): User = {}
```

but I would like a function

```kotlin
fun getUser(url: Url, userCallback: (User) -> Unit): Unit = {}
```

that is, a function that lets you subscribe to a user (directly!)

it would be written like this

```kotlin
val getUser(url: Url, userCallback: (User) -> Unit): Unit = {
    getJson(url) { json ->
        userCallback(toUser(json))
    }
}
```

and it would be used like this

```kotlin
getUser(url) { user ->
    // do things with the user
}
```

that is!

# future array

Let's say I have the function

```kotlin
fun getUser(url: Url, userCallback: (User) -> Unit): Unit = {}
```

and a array of urls

```kotlin
val urls = listOf("url1", "url2")
```

and would like a function like this

```kotlin
fun getUsers(urls: List<Url>, usersCallback: (List<User>) -> Unit): Unit = {}
```

I found myself without ```Promise.all``` so I had to use a workaround

From my experience with haskell, I noticed the solution was recursion

```kotlin
fun getUsers(urls: List<Url>, usersCallback: (List<User>) -> Unit): Unit = {
    getUsersRec(urls, usersCallback, listOf())
}

fun getUsersRec(urls: List<Url>, usersCallback: (List<User>) -> Unit, accumulation: List<User>): Unit = {
    if (urls.isEmpty) {
        // "return" all accumulated users
        usersCallback(accumulation)
    } else {
        // get one user
        getUser(urls.first) { user ->
            // accumulate the new user
            val newList = accumulation + listOf(user)
            // continue with list
            getUsersRec(urls.subList(1, urls.size), usersCallback, newList)
        }
    }
}
```

unlike ```Promise.all```, this function is sequential, not parallel, but it will work fine most cases
