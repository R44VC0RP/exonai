My apologies for the confusion. Since `selectedImage` is an optional, you need to unwrap it before calling the `getColors()` function. You can do this using optional binding:

```swift
if let selectedImage = selectedImage,
   let colors = selectedImage.getColors() {
    // ...
}
```

Here's the updated code for this section:

```swift
if let selectedImage = selectedImage, let colors = selectedImage.getColors() {
    Text("Primary Color: \(selectedColor?.toHexString() ?? "N/A")")
    HStack {
        Button(action: { selectedColor = colors.primary }) {
            RoundedRectangle(cornerRadius: 4)
                .fill(Color(colors.primary))
                .border(selectedColor == colors.primary ? Color.black : Color.clear)
        }
        Button(action: { selectedColor = colors.secondary }) {
            RoundedRectangle(cornerRadius: 4)
                .fill(Color(colors.secondary))
                .border(selectedColor == colors.secondary ? Color.black : Color.clear)
        }
        Button(action: { selectedColor = colors.detail }) {
            RoundedRectangle(cornerRadius: 4)
                .fill(Color(colors.detail))
                .border(selectedColor == colors.detail ? Color.black : Color.clear)
        }
    }
    .frame(width: 50, height: 50)
}
```
