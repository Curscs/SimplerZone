# Misc Types
---

A collection of smaller utility types the module uses.

## Definition
---
```luau
export type Shape = BoxShape | CylinderShape | SphereShape | WedgeShape | GroupShape | MeshShape
export type Disconnector = () -> ()
export type ZoneItems = {
	parts: {BasePart},
	models: {Model},
	players: {Player},
	attachments: {Attachment},
	pvinstances: {PVInstance},
}
export type ZoneItem = {
	part: BasePart?,
	model: Model?,
	player: Player?,
	attachment: Attachment?,
	pvinstance: PVInstance?,
}
```