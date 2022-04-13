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

Eventually projects get bigger: more swift files, xib files, assets, etc.

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
All of these questions normally should be a no, otherwise the view is already doing more than needed. This is a standard check but not necessarily must be true 100% of times.
</aside>

<!-- > -->

## The controller

The least reusable part of an app 😰. Controllers are often very 
specific to the application they were written for. 

What are its responsibilities? It's basically the brains 🧠 of the app.

- Order of method calls.
- Refreshing the app.
- Presenting new views.
- Sending object between views.
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
used handle events. Typically this might be handling button taps. It is 
also used to handle system events like loading data. 

In a nutshell the observer pattern allows you to gave one object register 
for events that occur at another object. 

<!-- > -->

## Navigation on iOS

Usually navigation is handled by a `UINavigationController`. The 
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

This about a web browser, it's back button and history. The navigation 
controller works in the same way. 

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
Objective-C layer of the app. You're writting code in Swift but underneath 
it all there is a layer of Objective-C code doign some of the work. 

https://www.hackingwithswift.com/example-code/language/what-is-the-objc-attribute

### Use the Observer pattern

Here you will register an object and a method to call when an event occurs. 

The `button` will issue the event and call the `didTapButton` method when 
the `touchUpInside` event occurs. 

Add the following to `viewDidLoad`:

```Swift
button.addTarget(self, action: #selector(didTapButton), for: .touchUpInside)
```

The first parameter `self` is the target. This is object that owns the method
or "action". 

The "action" is the method to call on. You need to wrap the method 
name in `#selector()` because it will be called on the Objective-C layer. 

Last, the event that will trigger the action is "touchUpInside". This method 
occurs when you touch a button then break contact with the screen. 

In summary, you touch the button and lift your finger, the button wants to 
notify it's observers, it looks for the action at the target. In our 
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

The title property sets a title that a view controller displays at the top of it's view. 

You also setup an observer to listen for taps at the button. 

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

You made a new instance of `UINavigationController`, and set the 
`rootViewController`. 

Then you set the `modalPresentationStyle` style. This determines how 
our navigation controller will be displayed, `fullScreen` means it 
will completely cover it's parent view. 

Last, you present the navigation controller. 

It's important to understand that ViewController is presenting a
new view that is the navigation controller, and the navigation 
controller is displaying it's root view controller. 

```
- ViewController
    - navVC (UINavigationController)
        - rootVC (HelloViewController)
```

Any view controller can display another view controller. If need 
to navigate between views then we need a navgation controller. 

### Add another view to navigation stack

So far you should have a main view with a button that displays a 
navigation controller when tapped. The navigation controller 
displays a single root view. 

In this step you will add a new view to navigation controller and 
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

<!-- > -->

## Additional Resources

[Apple Documentation on MVC](https://developer.apple.com/library/content/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html)<br>
[About App Development with UIKit](https://developer.apple.com/documentation/uikit/about_app_development_with_uikit)<br>
[MVC analogy](https://medium.freecodecamp.org/model-view-controller-mvc-explained-through-ordering-drinks-at-the-bar-efcba6255053)<br>
[More on MVC](https://codeburst.io/mvc-design-pattern-analogy-to-an-old-school-landline-3dcd2e994063)<br>
[Wikipedia - architectural pattern](https://en.wikipedia.org/wiki/Architectural_pattern)
[MVC tutorial with networking](https://www.raywenderlich.com/1000705-model-view-controller-mvc-in-ios-a-modern-approach)
[Manual Navigation - article](https://medium.com/whoknows-swift/swift-the-hierarchy-of-uinavigationcontroller-programmatically-91631990f495)


----------------------------

<!-- > -->

<!-- ## Agenda

- MVC
- Organizing our project
- Working without a storyboard
- Navigation programmatically
- Extending our project -->

<!-- > -->

<!-- ## Learning Objectives

By the end of this lesson, students should be able to:

- Describe and use **MVC** in an Xcode project
- Implement **navigation programmatically**
- **Send information** between view controllers programmatically -->

<!-- > -->

<!-- ## Architectural Patterns

Eventually projects get bigger: more swift files, xib files, assets, etc.

If we are not careful we'll end up with **spaghetti code** 🍝
- without structure
- difficult to follow
- hard to maintain

We can avoid this by using an **architectural pattern**. -->

<!-- v -->

<!-- **"An architectural pattern is a general, reusable solution to a commonly occurring problem in software architecture within a given context"** -->

<!-- v -->

<!-- ## MVC

MVC is Apple's recommended architecture for iOS apps.

It's made up of three main objects:
- **The Model:** Where your data lives.
- **The View:** What the user sees.
- **The Controller:** Mediator between the view and the model. -->

<!-- v -->

<!-- <img src="https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/Art/model_view_controller_2x.png"> -->

<!-- v -->

<!-- <img src="https://docs-assets.developer.apple.com/published/4e7c26b6ad/ff7aa08f-4857-44ce-88d5-7dacbef84509.png"> -->

<!-- > -->

<!-- ## The model

- Model Objects (classes, structs, etc) -->

<!-- > -->

<!-- ## The view

Often reusable and doesn't handle any business logic.

- UIView subclasses

How to know if we are doing views right?

Does it interact with the model layer?<br>
Does it contain any business logic?<br>
Does it try to do anything not related to UI?<br>

<aside class="notes">
All of these questions normally should be a no, otherwise the view is already doing more than needed. This is a standard check but not necessarily must be true 100% of times.
</aside> -->

<!-- > -->

<!-- ## The controller

The least reusable part of an app 😰

What are its responsibilities? It's basically the 🧠 of the app.

- Order of method calls.
- Refreshing the app.
- Presenting new views.
- Sending object between views.
- Handle user interaction (What happens after the user taps a button?) -->

<!-- > -->

<!-- ## In Class Activity (10 min)

From what you just learned, draw your own version of the MVC diagram and review the responsibilities for each component.

**Can you explain it using a real world scenario with an analogy?**

[Jamboard Link](https://jamboard.google.com/d/1jXM7Lj9jtIjddtC-dM9ii3hLQLusiVo4f970mrfwUyE/edit?usp=sharing) -->

<!-- > -->

<!-- ## File Structure

You can take your Subscription Box project and arrange your files with MVC in mind.

1. Right click on the project navigator → New Group
2. Move files accordingly -->

<!-- v -->

<!-- ![files](assets/fileStructure.png) -->

<!-- > -->

<!-- ## Navigation

So far we've been building apps with one screen. Most of the time you will need to interact with two screens or more, and we should handle these transitions.

- Navigation can be done using Segues or programmatically. We'll cover the second option.

Follow along with the [Starter Code](https://github.com/amelinagzz/mvc-starter/tree/master) -->

<!-- > -->

<!-- ## Navigation Programmatically

Steps to setup a project with without a Storyboard.

1. Delete the storyboard file.
2. Remove the storyboard name on Project Navigator > Select Project > General > Deployment Info > Main Interface
3. Remove the Storyboard name from the .plist
3. Change the SceneDelegate to tell our app what to use as the initial ViewController. -->

<!-- > -->

<!-- ```swift
func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        guard let windowScene = (scene as? UIWindowScene) else { return }
        window = UIWindow(frame: UIScreen.main.bounds)
        let viewController = //An instance of your view controller goes here
        window?.rootViewController = viewController
        window?.makeKeyAndVisible()
        window?.windowScene = windowScene
    }
```
<aside class="notes">
Programmatically we defined an instance of the view controller and set it as the root view controller of the main window.
</aside> -->

<!-- > -->

<!-- Changing the `rootViewController` from another View Controller:

```swift
self.view.window!.rootViewController = //Instance of the VC you want to set as root
``` -->

<!-- > -->

<!-- ## Creating a Navigation Controller

When using the storyboard, we would embed view controllers in navigation controllers in the interface builder.

We can also do it programmatically:

```swift
let navigationController = UINavigationController(rootViewController: //some VC)
self.view.window!.rootViewController = navigationController -->

<!-- //or

present(navigationController, animated: true, completion: nil) present it on top of an existing VC

```

Having a navigation controller gives us a navigation bar and the stack to show and dismiss view controllers. -->

<!-- > -->

<!-- ### Presenting a VC with the sliding left animation

```swift
let nextVC = ViewController()
self.navigationController?.pushViewController(nextVC, animated: true)
``` -->

<!-- > -->

<!-- ### Presenting a VC with the sliding up animation

```swift
let nextVC = ViewController()
self.navigationController?.present(nextVC, animated: true, completion: nil)
``` -->

<!-- > -->


<!-- ### Dismissing a View Controller to go back to a previous screen

If you used the **present** method:

```swift
self.dismiss(animated: true, completion: nil)
```

If you used the **push** method:

```swift
self.navigationController?.popViewController(animated: true)
``` -->

<!-- > -->

<!-- Return to root:

```swift
self.navigationController?.popToRootViewController(animated: true)
``` -->

<!-- > -->

<!-- ## Passing Information

We assign the value of properties right after creating the instance of the second view controller.

```swift
let nextVC = ViewController()
nextVC.color = UIColor.red //The instance of ViewController has a property called `color` and we are sending over the value `UIColor.red` to use it later in the next VC.
``` -->

<!-- > -->

<!-- ## Lab Time

[Activity Link](https://github.com/Make-School-Courses/MOB-1.2-Introduction-to-iOS-Development/blob/master/Lessons/05-Intro-to-MVC/assignments/navigation.md) -->

<!-- > -->

<!-- ### Changing rootViewController with an animation (cool thing to know)

Scenarios: <br>
The end of an onboarding flow.<br>
User logged out.


```swift
extension UINavigationController {
    /**
     It removes all view controllers from navigation controller then set the new root view controller and it pops.

     - parameter vc: root view controller to set a new
     */
    func initRootViewController(vc: UIViewController, transitionType type: String = "kCATransitionFade", duration: CFTimeInterval = 0.3) {
        self.addTransition(transitionType: type, duration: duration)
        self.viewControllers.removeAll()
        self.pushViewController(vc, animated: false)
        self.popToRootViewController(animated: false)
    }

    /**
     It adds the animation of navigation flow.

     - parameter type: kCATransitionType, it means style of animation
     - parameter duration: CFTimeInterval, duration of animation
     */
    private func addTransition(transitionType type: String = "kCATransitionFade", duration: CFTimeInterval = 0.3) {
        let transition = CATransition()
        transition.duration = duration
        transition.timingFunction = CAMediaTimingFunction(name: CAMediaTimingFunctionName.easeInEaseOut)
        transition.type = CATransitionType(rawValue: type)
        self.view.layer.add(transition, forKey: nil)
    }
}
``` -->

