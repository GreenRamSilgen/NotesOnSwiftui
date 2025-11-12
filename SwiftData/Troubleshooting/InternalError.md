# Internal Errors

If swift gives you @StorageRestriction and no other error it might be because an enum you used does not conform to whatever PROTOCOLS it needs.
**Original, Enum only has String**

```swift
@Model {
    var accountType : AccountTypes
    { @storageRestrictions(accesses: _$backingData, initializes: _accountType) init(initialValue) { _$backingData.setValue(forKey: \.accountType, to: initialValue) _accountType = _SwiftDataNoType() } get { _$observationRegistrar.access(self, keyPath: \.accountType) return self.getValue(forKey: \.accountType) } set { _$observationRegistrar.withMutation(of: self, keyPath: \.accountType) { self.setValue(forKey: \.accountType, to: newValue) } } }
}

enum AccountTypes : String {
    case checking
    case saving
}

```

**Fixed, Enum has Codable and CaseIterable**

```swift
@Model {
    var accountType : AccountTypes
}

enum AccountTypes: String, Codable, CaseIterable {
    case checking
    case saving
}

## Key points

- You may not need to go about deleting swiftData stores and other storage. Just update enum or other data types
