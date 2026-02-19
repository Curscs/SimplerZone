# Zone
---

`Zone`s are the main object of the `SimplerZone` library. `Zone`s are composed of `ShapeInstance`s and contain methods to manipulate/use them.

## Definition
---
```luau
{
	getRandomPoint: (Zone) -> vector,
	isPointInZone: (Zone, point: vector) -> boolean,
	isBoxInZone: (Zone, cframe: CFrame, size: vector) -> boolean,
	rebuild: (Zone) -> (),
	rebuildIfDirty: (Zone) -> (),
	
	shapes: {ShapeInstance},
	bvh: Geometry.BvhNode,
	boxes: {Geometry.Box},
	bvhDirty: boolean,
}
```

## Methods
---

### Zone:getRandomPoint() -> vector

Returns a random point inside any of the `ShapeInstance`s this `Zone` is composed of.

### Zone:isPointInZone(point: vector) -> boolean

Checks if `point` is inside any of the `ShapeInstance`s this `Zone` is composed of.

### Zone:isBoxInZone(cframe: CFrame, size: vector) -> boolean

Checks if a box, defined by `cframe` and `size`, is inside any of the `ShapeInstance`s this `Zone` is composed of.

### Zone:rebuild() -> ()

Rebuilds the static geometry of this `Zone`. Should be called if any of the `ShapeInstance`s this `Zone` is composed of is mutated in some way.

### Zone:rebuildIfDirty() -> ()

Calls `Zone:rebuild()` if `Zone.bvhDirty` is true.

## Fields
--

### Zone.shapes: {ShapeInstance}

The `ShapeInstance`s this `Zone` is composed of.

### Zone.bvh: BvhNode

The root `BvhNode` this `Zone` uses to optimize bounds checking.

### Zone.bvhDirty: boolean

If `Zone.bvh` should be rebuilt at some point.

### Zone.boxes: {Box}

The bounding box of each `ShapeInstance` in `Zone.shapes`.