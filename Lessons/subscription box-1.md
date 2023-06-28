# Subscription Box Login Screen

Create a login in screen. Take a look at the mockups for the subscription box. Look at the login screen. 

https://scene.zeplin.io/project/5e3b505d29276dd08ba41cc1

Let's mock this up as a SwiftUI View. 

There are a couple elements here.

- The title of the app
- A picture 
- The username text field 
- The password text field
- and the login button

Start with a `VStack` since the elements fit on the screen and are arranged in a vertical column. 

```Swift
struct LoginView: View {
  var body: some View {
    VStack {
      
    }
  }
}
```

Add the title

```Swift
struct LoginView: View {
  var body: some View {
    VStack {
      Text("Pet Box")
    }
  }
}
```

Follow the guide here to style the title: https://sarunw.com/posts/swiftui-text-font/

Next add an image. 

```Swift
struct LoginView: View {
  var body: some View {
    VStack {
      Text("Pet Box")
        .font(.system(size: 60, weight: .bold))
      Image(systemName: "pawprint")
    }
  }
}
```

You can import an image, I'm using a system image. 

Follow the guide here: https://codewithchris.com/swiftui/swiftui-image/

Style the image to get it where you like it. 

Now add some text fields. 

```Swift
struct LoginView: View {
  @State var username: String = ""
  @State var password: String = ""
  var body: some View {
    VStack {
      Text("Pet Box")
        .font(.system(size: 60, weight: .bold))
      Image(systemName: "pawprint")
        .resizable()
        .frame(width: 120, height: 120)
      TextField("username", text: $username)
      TextField("password", text: $password)
    }
  }
}
```

You need two `@State` variables, one for each `TextField`. This is the two lines at the top: 

```Swift 
@State var username: String = ""
@State var password: String = ""
```

These are used in the two `TextFields`: 

```Swift 
TextField("username", text: $username)
TextField("password", text: $password)
```

This sets up the text fields. Style them! Follow the guide here: 

https://thehappyprogrammer.com/custom-textfield-in-swiftui

Last, add a button. 

```Swift 
struct LoginView: View {
  @State var username: String = ""
  @State var password: String = ""
  var body: some View {
    VStack {
      Text("Pet Box")
        .font(.system(size: 60, weight: .bold))
      
      Image(systemName: "pawprint")
        .resizable()
        .frame(width: 120, height: 120)
      
      TextField("username", text: $username)
        .textFieldStyle(OvalTextFieldStyle())
        .padding()
      TextField("password", text: $password)
        .textFieldStyle(OvalTextFieldStyle())
        .padding()
      Button("Login") {
        print("Login!!!!")
      }
    }
  }
}
```

Style the button. Follow the guide here: 

https://www.fivestars.blog/articles/button-styles/






