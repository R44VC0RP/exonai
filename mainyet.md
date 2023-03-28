From the code snippet you provided, I cannot find the CoreData setup for the `ClothingItemEntity`. However, I can help you set it up correctly. First, make sure you've created a CoreData data model file (`ClothingItemModel.xcdatamodeld`) containing the `ClothingItemEntity` entity with the following attributes:

1. clothingname (type String)
2. itemImageData (type Binary Data)
3. temperature (type Double)

If you haven't done that, open your Xcode project, go to `File > New > File...` and select `Data Model` under the Core Data category. Then, create the entity and add the attributes as mentioned above.

Next, update your `PersistenceController` to match the name of the data model file:

```swift
init() {
    container = NSPersistentContainer(name: "ClothingItemModel") // Make sure to use the name of your data model file
    container.loadPersistentStores(completionHandler: { (storeDescription, error) in
        if let error = error as NSError? {
            fatalError("Unresolved error \(error), \(error.userInfo)")
        }
    })
}
```

In your `ClosetView`, you need to change the way you load and save the clothing items to use CoreData instead of an array of `ClothingItem`. Here's an example of how you can achieve that:

```swift
// Add this fetch request to load clothing items from CoreData
@FetchRequest(
    entity: ClothingItemEntity.entity(),
    sortDescriptors: [NSSortDescriptor(keyPath: \ClothingItemEntity.clothingname, ascending: true)]
) private var clothingItems: FetchedResults<ClothingItemEntity>
```

Now, to save a new clothing item to CoreData, you can create a function like this:

```swift
func saveClothingItem(name: String, temperature: Double, imageData: Data) {
    let newItem = ClothingItemEntity(context: container.viewContext)
    newItem.clothingname = name
    newItem.temperature = temperature
    newItem.itemImageData = imageData

    do {
        try container.viewContext.save()
    } catch {
        print("Error saving new item: \(error.localizedDescription)")
    }
}
```

To delete a clothing item, you can use the following function:

```swift
func deleteClothingItem(item: ClothingItemEntity) {
    container.viewContext.delete(item)

    do {
        try container.viewContext.save()
    } catch {
        print("Error deleting item: \(error.localizedDescription)")
    }
}
```

Update the `AddItemView` and `ClothingItemDetails` to use the new `saveClothingItem` and `deleteClothingItem` functions accordingly.

With these changes, you should be able to fetch, save, and delete clothing items using CoreData. If you still encounter issues, please provide more details, such as logs or error messages, to help identify the problem.
