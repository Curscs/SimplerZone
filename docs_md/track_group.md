# TrackGroup
---

`TrackGroup`s are containers that contain items that `ZoneListener`s should be tracking for when they enter/exit the `Zone`s it's listening to.

## Definition
---
```luau
{
	update: (TrackGroup) -> (),
	removeFrom: (TrackGroup, listener: ZoneListener) -> (),
	addItem: (TrackGroup, item: ZoneItem) -> (),
	addItems: (TrackGroup, items: ZoneItems) -> (),
	removeItem: (TrackGroup, item: ZoneItem) -> (),
	removeItems: (TrackGroup, items: ZoneItems) -> (),
	clear: (TrackGroup) -> (),
	
	mutable: ZoneItems,
	immutable: ZoneItems,
	listeners: {ZoneListener}
}
```

## Methods
---

### TrackGroup:update() -> ()

Moves items inside `TrackGroup.mutable` into `TrackGroup.immutable`, updating any listeners in the process.

### TrackGroup:removeFrom(listener: ZoneListener)

Removes this `TrackGroup` from the `listener`, making it no longer tracked for that listener.

### TrackGroup:addItem(item: ZoneItem) -> ()

Tracks the items inside `ZoneItem`, updating any listeners in the process.

### TrackGroup:addItems(item: ZoneItems) -> ()

Tracks the items inside `ZoneItems`, updating any listeners in the process.

### TrackGroup:removeItem(item: ZoneItem) -> ()

Untracks the items inside `ZoneItem`, updating any listeners in the process.

### TrackGroup:removeItems(items: ZoneItems) -> ()

Untracks the items inside `ZoneItems`, updating any listeners in the process.

### TrackGroup:clear() -> ()

Removes all tracked items within this `TrackGroup`.

## Fields
---

### TrackGroup.mutable: ZoneItems

A mutable list of tracked items that have not yet been registered into listeners.

### TrackGroup.immutable: Zoneitems

An immutable list of tracked items that have been registered into listeners.

### TrackGroup.listeners: {ZoneListener}

All `ZoneListener`s currently tracking this `TrackGroup`.