# Build a Basic Calculator App with SwiftUI

> **Target audience:** ACS 2420 students who have finished SwiftUI basics.
> **Goal:** In \~60 minutes, produce a fully functional four‑function calculator (add, subtract, multiply, divide) for iPhone.

---

## 🗺️ Tutorial Roadmap

| Step | Focus                        | Time   | Outcome                                    |
| ---- | ---------------------------- | ------ | ------------------------------------------ |
| 1    | Project Setup                | 5 min  | Xcode project ready, app runs blank screen |
| 2    | Laying Out Buttons & Display | 15 min | Number grid & display stack appear         |
| 3    | State & Input Handling       | 15 min | Tapping buttons updates display            |
| 4    | Calculation Engine (Model)   | 10 min | Operations (+ − × ÷) produce results       |
| 5    | Polishing UI                 | 10 min | Fancy colors, dark‑mode friendly           |
| 6    | Stretch Goals                | —      | Percentage, +/- toggle, haptics            |

---

## 1. Project Setup

1. **File → New → iOS App** → Interface: **SwiftUI**, Language: **Swift**.
2. App name `CalculatorSwiftUI`.
3. Build & run; you should see the default *Hello, world!*.

> **Checkpoint A**: Commit `git init` + first commit.

---

## 2. UI Layout (View)

### a. Replace `ContentView`

```swift
struct ContentView: View {
    @State private var display = "0"
    let buttons: [[CalcButton]] = [
        [.clear, .plusMinus, .percent, .operation("÷")],
        [.digit("7"), .digit("8"), .digit("9"), .operation("×")],
        [.digit("4"), .digit("5"), .digit("6"), .operation("−")],
        [.digit("1"), .digit("2"), .digit("3"), .operation("+")],
        [.digit("0"), .decimal, .equals]
    ]

    var body: some View {
        VStack(spacing: 12) {
            Spacer()
            // Display
            Text(display)
                .font(.largeTitle)
                .frame(maxWidth: .infinity, alignment: .trailing)
                .padding()
            // Buttons
            ForEach(buttons, id: \ .self) { row in
                HStack(spacing: 12) {
                    ForEach(row) { button in
                        CalculatorButton(button: button) {
                            handleTap(button)
                        }
                    }
                }
            }
        }
        .padding()
    }
}
```

### b. `CalcButton` Enum & View

```swift
enum CalcButton: Hashable, Identifiable {
    case digit(String)
    case operation(String)
    case decimal, equals, clear, plusMinus, percent
    
    var id: Self { self }
    var title: String {
        switch self {
        case .digit(let value): return value
        case .operation(let op): return op
        case .decimal: return "."
        case .equals: return "="
        case .clear: return "AC"
        case .plusMinus: return "±"
        case .percent: return "%"
        }
    }
    var background: Color {
        switch self {
        case .operation: return .orange
        case .clear, .plusMinus, .percent: return Color(.lightGray)
        default: return Color(.darkGray)
        }
    }
}

struct CalculatorButton: View {
    let button: CalcButton
    let action: () -> Void

    var body: some View {
        Button(action: action) {
            Text(button.title)
                .font(.title)
                .frame(width: buttonWidth(button), height: buttonWidth(button))
                .background(button.background)
                .foregroundColor(.white)
                .cornerRadius(buttonWidth(button) / 2)
        }
    }
    private func buttonWidth(_ item: CalcButton) -> CGFloat {
        let screen = UIScreen.main.bounds.width
        return item == .digit("0") ? (screen - 5 * 12) / 2 : (screen - 5 * 12) / 4
    }
}
```

> **Checkpoint B**: UI grid renders; buttons highlight when tapped (no logic yet).

---

## 3. State & Input Handling (ViewModel)

Add simple state vars & tap logic **inside `ContentView`**:

```swift
@State private var currentNumber = "0"
@State private var previousNumber: Double? = nil
@State private var currentOperation: CalcButton? = nil

func handleTap(_ button: CalcButton) {
    switch button {
    case .digit(let value):
        currentNumber = currentNumber == "0" ? value : currentNumber + value
        display = currentNumber
    case .decimal:
        if !currentNumber.contains(".") { currentNumber += "." }
        display = currentNumber
    case .operation:
        previousNumber = Double(currentNumber)
        currentOperation = button
        currentNumber = "0"
    case .equals:
        performCalculation()
    case .clear:
        currentNumber = "0"; previousNumber = nil; currentOperation = nil; display = "0"
    default: break // plusMinus, percent – stretch
    }
}

func performCalculation() {
    guard let operation = currentOperation, let prev = previousNumber, let curr = Double(currentNumber) else { return }
    let result: Double
    switch operation {
    case .operation("+"): result = prev + curr
    case .operation("−"): result = prev - curr
    case .operation("×"): result = prev * curr
    case .operation("÷"): result = prev / curr
    default: return
    }
    display = String(result)
    currentNumber = display
    currentOperation = nil
}
```

> **Checkpoint C**: Calculator performs + − × ÷ with integers / decimals.

---

## 4. Polish (Optional)

* Add `.shadow(radius:3)` to button.
* Use `.preferredColorScheme(.dark)` in preview.
* Add haptics: `UIImpactFeedbackGenerator(style:.light).impactOccurred()` inside `handleTap`.

---

## 5. Stretch Goals

* Implement ± toggle, `%` percentage.
* Landscape two‑column layout with `LazyVGrid`.
* Unit tests for `performCalculation()`.

---

## ✅ Wrap‑up

You’ve built a SwiftUI calculator with:

* **Grid layout** via nested `ForEach` loops.
* **Enum‑driven buttons** for clean data & styling.
* **@State** for simple MVVM.

Push to GitHub, tag `v1.0`, and show your working app!
