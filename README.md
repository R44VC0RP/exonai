You can achieve this by using a `@State` property to store the selected color and updating it when the user taps on a color rectangle. Here's how you can modify the `AddItemView` to allow the user to select one of the colors:

1. Add a new state property to store the selected color:

```swift
@State private var selectedColor: UIColor?
```

2. Update the color rectangles to act as buttons and change the selected color when tapped:

```swift
if let colors = selectedImage.getColors() {
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

3. In the "Add" button's action, use the `selectedColor` instead of extracting the primary color again:

```swift
.navigationBarItems(leading: Button("Cancel") {
    dismiss()
}.foregroundColor(Color.cyan), trailing: Button("Add") {
    let imageData = selectedImage?.jpegData(compressionQuality: 1.0)
    
    let newItem = ClothingItem(clothingname: selectedItem, temperature: temperatureRating, itemImageData: imageData, primaryColor: selectedColor)
    
    onAdd(newItem)
    dismiss()
}.foregroundColor(Color.cyan))
```

Now, the user can select one of the colors from the top three colors extracted from the image, and the selected color will be used as the primary color for the `ClothingItemEntity`. A black border will be displayed around the selected color to indicate the user's choice.
