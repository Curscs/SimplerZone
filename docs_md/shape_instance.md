# ShapeInstance
---

If `Shape`s were akin to Mesh Ids, then `ShapeInstance`s would be MeshParts.

`ShapeInstance`s define an instance of a `Shape`, specifying its world `.cframe`, and `.scale`.

## Definition
---
```luau
{
    toParts: (ShapeInstance, overrideCFrame: CFrame?) -> {BasePart},
	syncWithPart: (ShapeInstance, part: BasePart) -> Disconnector,
	syncWithAttachment: (ShapeInstance, attachment: Attachment) -> Disconnector,
	attach: (ShapeInstance, zone: Zone) -> (),
	detach: (ShapeInstance) -> (),
	
	cframe: CFrame,
	scale: vector,
	zones: {Zone},
	shape: Shape,
}
```

## Methods
---

### ShapeInstance:attach(zone: Zone) -> ()

Attaches this `ShapeInstance` to `zone`, adding to its geometry.

### ShapeInstance:detach(zone: Zone) -> ()

Removes this `ShapeInstance` from the `zone`, removing from its geometry.

### ShapeInstance:detachAll() -> ()

Removes this `ShapeInstance` from all attached `zone`s

### ShapeInstance:toParts(overrideCFrame: CFrame? = CFrame.identity) -> {BasePart}

Creates an array of `BasePart`s from a `ShapeInstance`. The world CFrame will be centered around `overrideCFrame`

### ShapeInstance:syncWithPart(part: BasePart) -> ()

Syncs the `ShapeInstance` with a `BasePart`. When the `BasePart` moves, so does the `ShapeInstance`, updating any `Zone`s it's attached to.

### ShapeInstance:syncWithAttachment(attachment: Attachment) -> ()

Syncs the `ShapeInstance` with an `Attachment`. When the `Attachment` moves (`.WorldCFrame`), so does the `ShapeInstance`, updating any `Zone`s it's attached to.

## Fields
---

### ShapeInstance.shape: Shape

Defines the form/shape of this `ShapeInstance`.

### ShapeInstance.cframe: CFrame

The world `CFrame` of this `ShapeInstance`. The `.shape` field will be transformed by this fields value.

When mutating this field, make sure to call `Zone:rebuild()` on all `Zone`s inside `ShapeInstance.zones` so that the change registers properly.

### ShapeInstance.scale: vector

The scale modifier to apply to the `.shape` fields values size.

### ShapeInstance.zones: {Zone}

All `Zone`s that this `ShapeInstance` is attached to.