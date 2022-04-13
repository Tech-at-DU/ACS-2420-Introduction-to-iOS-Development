<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->

<!-- .slide: class="header" -->
# Model View Controller

<!-- ## [Slides](https://make-school-courses.github.io/MOB-1.2-Introduction-to-iOS-Development/Slides/05-Intro-to-MVC/README.html ':ignore') -->


<!-- > -->

## Learning Objectives

- Describe MVC

<!-- > -->

## Architectural Patterns

Eventually, projects get bigger: more swift files, xib files, assets, etc.

If we are not careful we'll end up with **spaghetti code** 🍝
- without structure
- difficult to follow
- hard to maintain

We can avoid this by using an **architectural pattern**.

<!-- > -->

**"An architectural pattern is a general, reusable solution to a commonly occurring problem in software architecture within a given context"**

<!-- > -->

## MVC

The MVC pattern is used to create user interfaces. MVC is Apple's 
recommended architecture for iOS apps.

It's made up of three main objects:
- **The Model:** Where your data lives.
- **The View:** What the user sees.
- **The Controller:** Mediator between the view and the model.

<!-- > -->

<img src="https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/Art/model_view_controller_2x.png">

<!-- > -->

<img src="https://docs-assets.developer.apple.com/published/4e7c26b6ad/ff7aa08f-4857-44ce-88d5-7dacbef84509.png">

<!-- > -->

## The model

Holds the data that will be displayed by the user interface. 

- Model Objects (classes, structs, etc)
- Array
- primitive types (strings, Int, Float, etc)

<!-- > -->

## The view

The view's job is to **display** data from the model. The view should never
update the model. 

Often reusable and doesn't handle any business logic.

- UIView subclasses

How to know if we are doing views right?

- Does not interact with the model layer!
- Does not contain any business logic!
- Does not try to do anything not related to UI!

<aside class="notes">
All of these questions normally should be a no, otherwise, the view is already doing more than needed. This is a standard check but not necessarily must be true 100% of the time.
</aside>

<!-- > -->

## The controller

The least reusable part of an app 😰. Controllers are often very 
specific to the application they were written for. 

What are its responsibilities? It's basically the brains 🧠 of the app.

- Order of method calls.
- Refreshing the app.
- Presenting new views.
- Sending objects between views.
- Handle user interaction (What happens after the user taps a button?)

<!-- > -->

## Other software design patterns

Are there other programming patterns? Yes! there are plenty! People have 
plenty of books on the subject. 

- https://en.wikipedia.org/wiki/Design_Patterns
- https://rubygarage.org/blog/swift-design-patterns

New patterns are also being invented. For example Reactive functional 
programming used by ReactJS. 

## Observer Pattern

The observer pattern appears in many places. The observer pattern is 
used to handle events. Typically this might be handling button taps. It is 
also used to handle system events like loading data. 

In a nutshell, the observer pattern allows you to give one object register 
for events that occur at another object. 

<!-- > -->

## Navigation on iOS

Usually, navigation is handled by a `UINavigationController`. The 
`UINavigationController` class manages a 'stack' of `UIViewControllers`. 
The 'stack' is an array. The navigation controller displays the 
view controller at the top of the stack. 

You can manage which view controller is displayed by adding and 
removing view controllers from the stack. We call this pushing
and popping. 

When you push a view controller, you are adding it to the top of the
stack and it should be displayed. 

When you pop a view controller you are removing it from the stack and
the previous view controller is displayed. 

This is about a web browser, its back button, and its history. The navigation 
the controller works in the same way. 

The root view controller is the first view controller on the stack. 
Every navigation controller needs a root view controller or there 
would be nothing to display!

<!-- > -->

## Try it out

Follow the steps here to build an app that uses MVC, Observer, and 
navigation controller. 

<!-- > -->

### Make a new XCode Project

Create a new Xcode Project. 

### Edit the View Controller 

Take a look at the default ViewController.swift. 

Define a button at the top of the class:

```Swift
let button: UIButton = {
    let button = UIButton()
    button.setTitle("Go to Next", for: .normal)
    button.backgroundColor = .darkGray
    button.setTitleColor(.white, for: .normal)
    button.frame = CGRect(x: 100, y: 100, width: 200, height: 60)
    return button
 }()
```

Note! Here you are creating and initializing a new `UIButton` with a 
closure/anonymous function.

In `viewDidLoad` change the background color, and add the button:

```Swift
view.backgroundColor = .green
view.addSubview(button)
```

Handle taps on the button by adding a method that can be called when
the button is tapped: 

```Swift
@objc func didTapButton() {
    print("Button Tapped!")
}
```

Note! We need to have @objc here because we want this method available to 
Objective-C layer of the app. You're writing code in Swift but underneath 
it all there is a layer of Objective-C code doing some of the work. 

https://www.hackingwithswift.com/example-code/language/what-is-the-objc-attribute

### Use the Observer pattern

Here you will register an object and a method to call when an event occurs. 

The `button` will issue the event and call the `didTapButton` method when 
the `touchUpInside` event occurs. 

Add the following to `viewDidLoad`:

```Swift
button.addTarget(self, action: #selector(didTapButton), for: .touchUpInside)
```

The first parameter `self` is the target. This is the object that owns the method
or "action". 

The "action" is the method to call on. You need to wrap the method 
name in `#selector()` because it will be called on the Objective-C layer. 

Last, the event that will trigger the action is "touchUpInside". This method 
occurs when you touch a button and then break contact with the screen. 

In summary, you touch the button and lift your finger, the button wants to 
notify its observers, it looks for the action at the target. In our 
example, it looks for `didTapButton` (action) at `self` (target.)

<!-- > -->

### Make a new View controller

Make a new ViewController. You will display this inside of a navigation 
 controller when the button is tapped. 

Create a new Sweift file: HelloViewController.swift

Add the following: 

```Swift
import UIKit

class HelloViewController: UIViewController {
    let button: UIButton = {
        let button = UIButton()
        button.setTitle("Go to Next", for: .normal)
        button.backgroundColor = .darkGray
        button.setTitleColor(.white, for: .normal)
        button.frame = CGRect(x: 100, y: 100, width: 200, height: 60)
        return button
    }()
 
    override func viewDidLoad() {
        super.viewDidLoad()
        title = "Hello"
        view.backgroundColor = .systemCyan
        view.addSubview(button)
        button.addTarget(self, action: #selector(didTapButton), for: .touchUpInside)
    }
    
    @objc func didTapButton() {
    
    }
}
```

This view controller defines a button and displays that button. 

The title property sets a title that a view controller displays at the top of its view. 

You also set up an observer to listen for taps at the button. 

### Create a Navigation controller

Back in ViewController. Add the following to `didTapButton`:

```Swift
let rootVC = HelloViewController()
let navVC = UINavigationController(rootViewController: rootVC)
navVC.modalPresentationStyle = .fullScreen
present(navVC, animated: true)
```

Here you made a new view controller, which will be displayed in the 
navigation controller. 

You made a new instance of `UINavigationController` and set the 
`rootViewController`. 

Then you set the `modalPresentationStyle` style. This determines how 
our navigation controller will be displayed, `fullScreen` means it 
will completely cover its parent view. 

Last, you present the navigation controller. 

It's important to understand that ViewController is presenting
 the view that is the navigation controller, and the navigation 
a controller is displaying its root view controller. 

```
- ViewController
    - navVC (UINavigationController)
        - rootVC (HelloViewController)
```

Any view controller can display another view controller. If need 
to navigate between views then we need a navigation controller. 

### Add another view to the navigation stack

So far you should have a main view with a button that displays a 
navigation controller when tapped. The navigation controller 
displays a single root view. 

In this step, you will add a new view to the navigation controller and 
display it. 

Create a new Swift File: WorldViewController.swift

Add the following: 

```Swift
import UIKit

class WorldViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        title = "World"
        view.backgroundColor = .yellow
    }
}
```

This creates a simple view controller with a title and a background color. 

In HelloViewController.swift add the following to the `didTapButton`
method: 

```Swift
let vc = WorldViewController()
navigationController?.pushViewController(vc, animated: true)
```

Here you made a new instance of WorldViewController and pushed 
it on to the navigation controllers navigation stack. 

### Dismissing the modal view

Our project's main view controller (ViewController) displays the 
navigation controller as a modal. A modal is a temporary view that 
appears in front of another view. 

Remember our structure: 

```
- ViewController
    - UINavigationController (displayed as modal)
        - rootVC (HelloViewController)
```

The modal view can be dismissed to reveal the original view 
controller that spawned it. When this happens the Navigation 
controller and all of the view controllers in its stack are 
removed together. 

In ViewController.swift. Add a new method:

```Swift
@objc func dismissSelf() {
    dismiss(animated: true)
}
```

This will dismiss a modal view that our view controller is displaying. 
You need to mark this `@objc` because you will call this method from 
a button. 

The navigation controller has a navigation bar and the navigation bar 
can host "bar button items". These special buttons live in the 
navigation bar. They are instances of the `UIBarButtonItem` class. 

In the `didTabButton` method add the following: 

```Swift
rootVC.navigationItem.rightBarButtonItem = UIBarButtonItem(
    title: "Dismiss",
    style: .plain,
    target: self,
    action: #selector(dismissSelf))
```

Here you added a new `UIBarButtonItem` to the Root view controller's 
navigation item right bar button item. 

The button is an instance of UIBarButtonItem and gets a title, style, target,
and action. This is very similar to what you did with the UIButton earlier.
The difference here is that this is a special button that lives in the 
navigation bar. 

### What's up with the navigation bar appearance? 

The navigation bar is a built object built from one of the UIKit classes. 
In iOS systems before 15, the navigation bar was not transparent. Instead,
it had a white semitransparent or colored background. 

iOS 15 gives the navigation bar a transparent appearance. Of course, you, 
as the app developer can control the appearance! 

You can customize the appearance of any of the UIKit elements in 
several ways. Earlier set the title on the navbar and created a navbar 
button and put it on the right of the bar. 

These changes were done locally on each view controller. Sometimes you'll 
want to set changes globally. All of the classes have a class method called 
`appearance()` for the purpose of defining global settings. 

Add the following to `didFinishLaunchingWithOptions` in AppDelegate.swift:

```Swift
if #available(iOS 15.0, *) {
    let navigationBarAppearance = UINavigationBarAppearance()
    navigationBarAppearance.configureWithDefaultBackground()
    UINavigationBar.appearance().standardAppearance = navigationBarAppearance
    UINavigationBar.appearance().compactAppearance = navigationBarAppearance
    UINavigationBar.appearance().scrollEdgeAppearance = navigationBarAppearance
}
```

The code here creates a `navigationBarAppearance` instance and set's its
properties to the default background appearance with: `configureWithDefaultBackground()`. Then assigns this object to some of 
the properties of `UINavigationBar.appearance()`.

Notice you're setting a method on the class object, not an instance! The 
class uses the properties stored here to initialize new instances. In this
way, all new instances will get the value you assign here when they are 
created. Since this, all happened in `didFinishLaunchingWithOptions` all 
of the elements your app creates will use these. 

<!-- > -->

## Additional Resources

[Apple Documentation on MVC](https://developer.apple.com/library/content/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html)<br>
[About App Development with UIKit](https://developer.apple.com/documentation/uikit/about_app_development_with_uikit)<br>
[MVC analogy](https://medium.freecodecamp.org/model-view-controller-mvc-explained-through-ordering-drinks-at-the-bar-efcba6255053)<br>
[More on MVC](https://codeburst.io/mvc-design-pattern-analogy-to-an-old-school-landline-3dcd2e994063)<br>
[Wikipedia - architectural pattern](https://en.wikipedia.org/wiki/Architectural_pattern)
[MVC tutorial with networking](https://www.raywenderlich.com/1000705-model-view-controller-mvc-in-ios-a-modern-approach)
[Manual Navigation - article](https://medium.com/whoknows-swift/swift-the-hierarchy-of-uinavigationcontroller-programmatically-91631990f495)

