# ZoneListener
---

A `ZoneListener` is an object that can listen to when certain items enter the geometric boundaries of a `Zone` defined by its `ShapeInstance`s.

## Definition
---
```luau
setmetatable<{
	onEnter: (ZoneListener, fn: (item: ZoneItem) -> ()) -> Disconnector,
	onExit: (ZoneListener, fn: (item: ZoneItem) -> ()) -> Disconnector,
	observe: (ZoneListener, fn: (item: ZoneItem) -> (() -> ())?) -> Disconnector,

	setGroups: (ZoneListener, groups: {TrackGroup}) -> (),

	subscribe: (ZoneListener, zone: Zone) -> (),
	unsubscribe: (ZoneListener, zone: Zone) -> (),
	unsubscribeAll: (ZoneListener) -> (),

	precision: "Part" | "BoundingBox",
	queryShape: "Point" | "Box",
	groups: {TrackGroup},
	zones: {Zone},
	itemsInside: ZoneItems,

	iter: (ZoneListener) -> () -> ZoneItem,
	data: ZoneListenerData
}, {__iter: (ZoneListener) -> () -> ZoneItem}>
```

## Methods
---

### ZoneListener:subscribe(zone: Zone) -> ()

Subscribes this `ZoneListener` to the `Zone`, making any item this listener is tracking who enters the geometric boundaries of the `Zone` fire events.

### ZoneListener:unsubscribe(zone: Zone) -> ()

Unsubscribes this `ZoneListener` from `zone`, cleaning up any internal listeners and events in the process.

### ZoneListener:unsubscribeAll() -> ()

Unsubscribes this `ZoneListener` from all `Zone`s it's subscribed to.

### ZoneListener:onEnter(fn: (item: ZoneItem) -> ()) -> Disconnector

Connects `fn` to be called when any `ZoneItem` enters the geometric boundaries of any subscribed `Zone`

### ZoneListener:onExit(fn: (item: ZoneItem) -> ()) -> Disconnector

Connects `fn` to be called when any `ZoneItem` exits the geometric boundaries of any subscribed `Zone`

### ZoneListener:observe(fn: (item: ZoneItem) -> (() -> ())?) -> Disconnector

Connects `fn` to be called when any `ZoneItem` enters the geometric boundaries of any subscribed `Zone`, and for the returned function (if any) to be called when it exits it. 

### ZoneListener:setGroups(groups: {TrackGroup}) -> ()

Sets the `TrackGroup`s that this `ZoneListener` should be listening for.