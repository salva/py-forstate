# forstate

The `forstate` module introduces the `for_state` method decorator,
designed to facilitate state-specific method dispatching.

This decorator enables the definition of multiple versions of the same
method, which are dynamically called based on the object's internal
state, as indicated by its `_state` attribute.

## Installation

You can easily install the `forstate` module via pip. Simply run the
following command in your terminal:

```
pip install forstate
```

## Usage

1. Import the `for_state` decorator and, if needed, the `ANY_STATE`
   sentinel to accommodate fallback methods.

2. Decorate your class methods with `@for_state`, specifying the
   relevant state names for each method. This enables you to define
   distinct behaviors for the same method name based on the object's
   current state.

3. Utilize the `ANY_STATE` marker to designate fallback methods that
   will be invoked when no specific version of a method is defined for
   the current state.


### Example

```python
from forstate import for_state, ANY_STATE

class MyStatefulObject:
    def __init__(self):
        self._state = "state0"  # Initial state

    @for_state("state1")
    def action(self):
        print("Action for state 1")

    @for_state("state2")
    def action(self):
        print("Action for state 2")

    @for_state(ANY_STATE)
    def action(self):
        print("Action for any state")

obj = MyStatefulObject()

obj._state = "state1"
obj.action()  # Output: Action for state 1

obj._state = "state2"
obj.action()  # Output: Action for state 2

obj._state = "unknown"
obj.action()  # Output: Action for any state
```

## Copyright and License

Copyright (c) 2025 Salvador Fandiño (sfandino@yahoo.com)

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.


