# RHSideButtons

## Play with it 😎
<iframe src="https://appetize.io/embed/zanve819jr7g7dmh326a924pq4?device=iphone6&scale=100&autoplay=false&orientation=portrait&deviceColor=black" width="416px" height="870px" frameborder="0" scrolling="no"></iframe>

## Usage
You just need implement `RHSideButtonsDataSource` and `RHSideButtonsDelegate` similar to well-known UIKit design.

```swift
// You need to firstly create trigger button. You can do this using block or your builder object which should conform to 'RHButtonViewConfigProtocol'
// RHTriggerButtonView allows you to change image for pressed state! 👌🏻
let triggerButton = RHTriggerButtonView(pressedImage: UIImage(named: "exit_icon")!) {
    $0.image = UIImage(named: "trigger_img")
    $0.hasShadow = true
}

// Then you need to create instance of SideButtons coordinator class with your View Controller view (it can be even TableView)
sideButtonsView = RHSideButtons(parentView: view, triggerButton: triggerButton)
sideButtonsView.delegate = self
sideButtonsView.dataSource = self

// When SideButtons controller is initialized properly you should set thier position in view in e.g. viewDidLoad method:
override func viewDidAppear(animated: Bool) {
    super.viewDidAppear(animated)

    sideBttns?.setTriggerButtonPosition(CGPoint(x: bounds.width - 85, y: frame.size.height - 85))
    sideButtonsView.reloadButtons()
}
```
```swift
//Finally you should create array of button which will feed our dataSource and Delegate methods :) e.g.:
let button_1 = RHButtonView {
    $0.image = UIImage(named: "icon_1")
    $0.hasShadow = true
}

let button_2 = RHButtonView {
    $0.image = UIImage(named: "icon_2")
    $0.hasShadow = true
}

let button_3 = RHButtonView {
    $0.image = UIImage(named: "icon_3")
    $0.hasShadow = true
}

buttonsArr.appendContentsOf([button_1, button_2, button_3])

//As it is in tableView, now you should reload buttons with new values
sideButtonsView.reloadButtons()
```

### RHSideButtonsDataSource
```swift
func sideButtonsNumberOfButtons(sideButtons: RHSideButtons) -> Int
func sideButtons(sideButtons: RHSideButtons, buttonAtIndex index: Int) -> RHButtonView
```

### RHSideButtonsDelegate
```swift
func sideButtons(sideButtons: RHSideButtons, didSelectButtonAtIndex index: Int)
func sideButtons(sideButtons: RHSideButtons, didTriggerButtonChangeStateTo state: RHButtonState)
```

<img src ="./Demo/RHSideButtons.gif" width="360" height="640"/>

## Support for left-handers :)
<img src ="./Demo/RHSideButtons_Left.gif" width="360" height="640"/>

If you decide to position RHSideButtons on the left site of view, buttons will dissapears to the left side of screen automatically.

e.g.:
```swift
sideBttns?.setTriggerButtonPosition(25, y: frame.size.height - 85))
```