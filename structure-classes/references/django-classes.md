# Django Classes

## No Type Switches

In a model hierarchy, put the varying behaviour on the base model as a method or property that each subclass overrides, instead of checking `isinstance` against the concrete models. For example, `MenuItem.preparation_minutes` is overridden by the `Pizza` and `Salad` models.
