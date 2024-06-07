# Liveness

## Installation

### Cocoapods

[CocoaPods](https://cocoapods.org) is a dependency manager for Cocoa projects. For usage and installation instructions, visit their website. To integrate RBKLiveness into your Xcode project using CocoaPods, specify it in your `Podfile`:

For iOS Swift projects:

```ruby
pod 'Liveness', :git => 'https://github.com/Salmik/LivenessLibrary', :tag => '1.0.3'
```

## Documentation
- [x] [Complete Documentation](https://salmik.github.io/LivenessLibrary/)


## Usage
You can create a view controller that will capture face:

```swift
let viewController = LivenessViewController(isRecordingEnabled: true) // isRecordingEnabled is false by default


// Delegate and DataSource
viewController.delegate = self
viewController.dataSource = self

present(viewController, animated: true)
```

Available customization:

```swift
viewController.titleColor = .black
viewController.titleFont = .systemFont(ofSize: 24)
viewController.descriptionColor = .lightGray
viewController.descriptionFont = .systemFont(ofSize: 14)
viewController.loadingText = "Loading..."
viewController.activityIndicatorColor = .gray
viewController.shouldSetMaxBrightness = true
```

Delegate methods:

```swift
extension YourViewController: LivenessDelegate {

    func liveness(didCaptureFaceIn image: UIImage) {}

    func liveness(willPassAction action: LivenessAction) {}

    func liveness(didPassActionWith result: LivenessResult) {}

    func liveness(didRecordVideoTo url: URL) {}

    func livenessDidSucceed() {}
}
```

DataSource methods: 

```swift
extension YourViewController: LivenessDataSource {

    func liveness(textForAlert alert: LivenessAlert) -> String? {
        // example
        switch alert {
        case .faceNotFound: return "Face not found"
        case .singleFace: return "There must be one person in the camera"
        ...
        }
    }

    func liveness(textForAction action: LivenessAction) -> String? {
        // example
        switch action {
        case .smile: return "Smile"
        case .turnLeft: return "Turn left"
        ...
        }
    }

    func liveness(descriptionTextForAction action: LivenessAction) -> String? {
        switch action {
        case .turnLeft: return "Slowly turn your head back and forth. Your face must remain in the camera's field of view"
        ...
        }
    }

    func liveness(textForPassedAction action: LivenessAction) -> String? { 
        return "Success" 
    }
}
```
