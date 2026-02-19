# Shape
---

A `Shape` is an elementary object that defines, well, the shape of your `Zone`s. `Shape`s aren't defined by `Instance`s with the exception of `MeshShape`, so you can create and use them even without explicitly making parts for them inside the workspace.

Most shapes will have a `.transform` property, this property determines the offset of the `Shape` from the `.cframe` of the `ShapeInstance` that uses it. In the case of `SphereShape`s, `.transform` isn't present and instead is replaced by `.center`

During usage of `Shape`s within `ShapeInstances`, it is gauranteed that the properties of your `Shape`s will not change. So it is okay to reference 1 `Shape` multiple times