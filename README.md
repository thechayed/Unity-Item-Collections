# Unity Item Collections
It's a List, but better.
# ItemCollection Class

The `ItemCollection<T>` class is an enhanced version of the standard `List<T>` in C#. It provides additional features and events to manage a collection of items, making it suitable for scenarios where you need to keep track of item additions and removals, enforce item limits, and perform various operations on the collection efficiently.

## Features

1. **Item Events**: `ItemCollection` includes two UnityEvents, `OnItemAdded` and `OnItemRemoved`, which allow you to register callbacks to be triggered when items are added or removed from the collection. This is useful for responding to changes in real-time.

2. **Item Indexing**: You can access items using indexers, both for retrieving a range of items and finding indices of items matching a specific value.

3. **Item Limit**: The `Max` property enables you to set a maximum item limit for the collection. If specified, attempts to add more items than the limit allows will be rejected.

4. **Item Addition and Removal**: Enhanced methods for adding, removing, and replacing items while invoking the corresponding events. This ensures you have control and notifications when manipulating the collection.

5. **Item Transfer**: You can transfer items between different `ItemCollection` instances, allowing for efficient management of items across multiple collections.

6. **Item Filtering**: Methods for removing items that match a certain condition or range, making it easier to filter and manipulate the collection based on specific criteria.

## Usage

```csharp
// Create an ItemCollection with a maximum limit of 100 items
ItemCollection<string> itemCollection = new ItemCollection<string>();
itemCollection.Max = 100;

// Register event handlers for item additions and removals
itemCollection.OnItemAdded.AddListener((index, item) =>
{
    Debug.Log($"Item added at index {index}: {item}");
});

itemCollection.OnItemRemoved.AddListener(item =>
{
    Debug.Log($"Item removed: {item}");
});

// Add items to the collection
itemCollection.Add("Item 1");
itemCollection.Add("Item 2");

// Retrieve items using indexers
List<string> itemsInRange = itemCollection[1..2];  // Get items at index 1 (inclusive) to index 2 (exclusive)

int[] indicesOfItem1 = itemCollection["Item 1"];  // Get indices of "Item 1"

// Remove items from the collection
itemCollection.Remove("Item 1");

// Transfer items from one collection to another
ItemCollection<string> anotherCollection = new ItemCollection<string>();
anotherCollection.Add("Another Item");

itemCollection.TransferAllFrom(anotherCollection);

// Replace an item at a specific index
itemCollection.Replace(0, "New Item");

// Remove items matching a condition
itemCollection.RemoveAll(item => item.Contains("Item"));

// Clear the entire collection
itemCollection.Clear();
```

The `ItemCollection` class enhances the standard `List` with additional functionality, making it a powerful tool for managing and manipulating collections of items in your Unity Projects.
