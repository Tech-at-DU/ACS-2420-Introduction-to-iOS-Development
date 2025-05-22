# ACS 2420 – Introduction to iOS Development

## Lesson 2: SwiftUI Basics – Views, Layout & State

---

### 🌐 Course Context

Last class you mastered core Swift. Today we jump into **SwiftUI**, Apple’s modern, declarative UI framework. By the end of this 3‑hour session you’ll build interactive views and understand the data‑flow that powers them.

---

## ✅ Learning Objectives

By the end of this lesson, you should be able to:

1. Explain the declarative nature of SwiftUI vs. UIKit/Storyboard.
2. Create and preview SwiftUI views in Xcode.
3. Use common layout containers (`VStack`, `HStack`, `ZStack`, `Spacer`).
4. Manage view state with `@State` and pass data with `@Binding`.
5. Build dynamic lists with `List` & `ForEach`.
6. Implement simple navigation using `NavigationStack` and `NavigationLink`.

---

## 📅 Agenda (3 hrs)

|  Time        |  Topic                                                   |
| ------------ | -------------------------------------------------------- |
|  0:00 – 0:15 |  Intro & review of declarative UI concepts               |
|  0:15 – 0:45 |  Live‑code **HelloSwiftUI** (Text, modifiers, Preview)   |
|  0:45 – 1:20 |  Layout deep‑dive: Stacks & Spacer + hands‑on challenges |
|  1:20 – 1:30 |  Break ☕                                                 |
|  1:30 – 2:00 |  `@State` Counter demo + state challenges                |
|  2:00 – 2:30 |  Lists & Navigation demo + challenges                    |
|  2:30 – 3:00 |  Share‑outs, Q\&A, wrap‑up                               |

---

## ✨ Part 1 – Your First SwiftUI View

```swift
import SwiftUI

struct HelloSwiftUIView: View {
    var body: some View {
        Text("👋 Hello, SwiftUI!")
            .font(.largeTitle)
            .padding()
    }
}

#Preview {
    HelloSwiftUIView()
}
```

> 💡 **Live‑code walkthrough**: create a new *iOS App* > *SwiftUI* in Xcode, paste the code, and watch the preview update instantly.

### Challenge A – Embellish the Greeting

Create a new view that shows your name in **bold**, colored **blue**, and rotated 5°.

---

## 📐 Part 2 – Layout with Stacks & Spacer

### Example

```swift
struct CardView: View {
    var body: some View {
        VStack(alignment: .leading, spacing: 12) {
            Text("SwiftUI Basics")
                .font(.headline)
            Text("Build UIs the modern way ✨")
                .font(.subheadline)
            HStack {
                Spacer()
                Text("🚀")
            }
        }
        .padding()
        .background(.yellow.opacity(0.3))
        .cornerRadius(12)
    }
}
```

### Challenge B – Profile Card

Build a vertical card that shows:

1. A circular avatar (`Image(systemName: "person.fill")`).
2. Your full name in title font.
3. A subtitle "iOS Learner" in gray.
4. Centered horizontally. Use stacks/spacers only—no hard‑coded frames.

---

## 🔄 Part 3 – State & Binding

### Example – Counter

```swift
struct CounterView: View {
    @State private var count = 0

    var body: some View {
        VStack(spacing: 20) {
            Text("Count: \(count)")
                .font(.title)
            HStack {
                Button("–") { count -= 1 }
                Button("+") { count += 1 }
            }
            .buttonStyle(.borderedProminent)
        }
    }
}
```

### Challenge C – Temperature Converter

Create a view with:

* A `TextField` for Celsius input (bind to `@State var celsius: Double`).
* A computed Fahrenheit value shown below (`(celsius * 9/5) + 32`).
* Keyboard type = `.decimalPad`.
* **Bonus**: Add `@FocusState` to dismiss keyboard on tap outside.

---

## 📋 Part 4 – Lists & Navigation

### Example

```swift
struct Todo: Identifiable { let id = UUID(); var title: String }

struct TodoListView: View {
    @State private var todos = [Todo(title: "Read docs"), Todo(title: "Write code")]

    var body: some View {
        NavigationStack {
            List($todos) { $todo in
                NavigationLink(todo.title) {
                    Text("Detail for \(todo.title)")
                }
            }
            .navigationTitle("Todos")
        }
    }
}
```

### Challenge D – Book Library List

1. Define a `Book` struct (`title`, `author`).
2. Display books in a `List` sorted alphabetically.
3. Tapping a row pushes a detail view showing both title & author.
4. Add a navigation bar button that appends a dummy book.

---

## 🧭 Why SwiftUI? (Discussion 5 min)

* Declarative mindset (similar to React)
* Live previews & hot‑reload feel
* Seamless theming (Dark Mode, Dynamic Type)
* Interoperability with UIKit via `UIViewControllerRepresentable`

---

## 🧪 AI Prompts (Optional, for early finishers)

* "Explain the difference between `@State` and `@Binding` with examples."
* "Generate three creative layouts using `ZStack` animations for a login screen."

---

## 🏁 After‑Class Resources

* Apple *SwiftUI Tutorials*: [https://developer.apple.com/tutorials/swiftui](https://developer.apple.com/tutorials/swiftui)
* Hacking with Swift *100 Days of SwiftUI* (Days 1–15 cover today’s topics).
* [Majid’s SwiftUI articles](https://swiftwithmajid.com)

> **Assignment**: Finish *Challenge D* and push to GitHub before next class.

---

## 🔜 Next Time

* SwiftUI Modifiers Deep‑Dive & Animations
