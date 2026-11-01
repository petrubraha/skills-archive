# Django Classes

## No Type Switches

In a model hierarchy, put the varying behaviour on the base model as a method or property that each subclass overrides, instead of checking `isinstance` against the concrete models. Examples: `Publication.author` and `PublicationActivity.bell_detail`.
