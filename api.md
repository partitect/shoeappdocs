Your first task will be to create a class that you can use to interact with the API.

Open your code editor and create a `http_service.dart` file in the `lib` directory. Here, you will develop a new `HttpService` class and add a `getPosts` function:

lib/http_service.dart

```
import 'dart:convert';
import 'package:http/http.dart';
import 'post_model.dart';

class HttpService {
  final String postsURL = "https://jsonplaceholder.typicode.com/posts";

  Future<List<Post>> getPosts() async {
    Response res = await get(postsURL);

    if (res.statusCode == 200) {
      List<dynamic> body = jsonDecode(res.body);

      List<Post> posts = body
        .map(
          (dynamic item) => Post.fromJson(item),
        )
        .toList();

      return posts;
    } else {
      throw "Unable to retrieve posts.";
    }
  }
}

```

In this example, you will be connecting to JSON Placeholder. This code uses the `http` package's `get` on the `postsURL` string.

If that request was successful, this code will return a `List<Post>` using `Post.fromJson`. Otherwise, an error message is thrown.

Note: [HTTP status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) are used to determine if a request was successful or unsuccessful. A status code of `200` represents a successful HTTP request.

Then, use your code editor to create a `post_model.dart` file in the `lib` directory. Here, you will develop a new `Post` class:

lib/post_model.dart

```
import 'package:flutter/foundation.dart';

class Post {
  final int userId;
  final int id;
  final String title;
  final String body;

  Post({
    @required this.userId,
    @required this.id,
    @required this.title,
    @required this.body,
  });

  factory Post.fromJson(Map<String, dynamic> json) {
    return Post(
      userId: json['userId'] as int,
      id: json['id'] as int,
      title: json['title'] as String,
      body: json['body'] as String,
    );
  }
}

```

In order to serialize the response from JSON Placeholder, this code will return a new `Post` with the `fromJson` method based on a JSON `Map`.

Note: In a production application, a package like [`json_serializable`](https://pub.dev/packages/json_serializable) could be used to handle the serialization automatically.

A `Post` returned by JSON Placeholder will consist of a `userId`, `id`, `title`, and `body`.

[Step 3 --- Displaying `Posts`](https://www.digitalocean.com/community/tutorials/flutter-flutter-http#step-3-displaying-posts)[](https://www.digitalocean.com/community/tutorials/flutter-flutter-http#step-3-displaying-posts)
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Next, use your code editor to create a `posts.dart` file in the `lib` directory. Here, you will create a `PostsPage` class which will display the `Posts` that are returned from the HTTP request to JSON Placeholder:

lib/posts.dart

```
import 'package:flutter/material.dart';
import 'http_service.dart';
import 'post_model.dart';

class PostsPage extends StatelessWidget {
  final HttpService httpService = HttpService();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Posts"),
      ),
      body: FutureBuilder(
        future: httpService.getPosts(),
        builder: (BuildContext context, AsyncSnapshot<List<Post>> snapshot) {
          if (snapshot.hasData) {
            List<Post> posts = snapshot.data;
            return ListView(
              children: posts
                  .map(
                    (Post post) => ListTile(
                      title: Text(post.title),
                      subtitle: Text("${post.userId}"),
                    ),
                  )
                  .toList(),
            );
          } else {
            return Center(child: CircularProgressIndicator());
          }
        },
      ),
    );
  }
}

```

This code uses the `FutureBuilder` widget to interact with the `getPosts()` function. This allows the code to determine when the `List<Post>` is ready and act accordingly.

If the `snapshot.hasData` is `false`, then the `CircularProgressIndicator` is displayed. Otherwise, the `ListTile` with post information is displayed.

In order to observe what you have so far, you will need to replace the code in `main.dart`.

Open `lib/main.dart` in your code editor and modify it to use `PostsPage`:

lib/main.dart

```
import 'package:flutter/material.dart';
import 'posts.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'HTTP',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: PostsPage(),
    );
  }
}
```