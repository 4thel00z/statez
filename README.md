# statez

![statez.png](https://raw.githubusercontent.com/4thel00z/logos/master/statez.png)

## Motivation

All the statemachine packages for python look weird and do too much stuff.
This one is simple (and synchronous).


## Installation

```
pip install statez

# or if you use poetry
poetry add statez
```

## Usage

```python
from statez import (
    Trigger,
    From,
    To,
    Do, StateMachine
)

if __name__ == '__main__':
    s = StateMachine("Flow1")
    transition = Trigger("on") | From(["from", "from2"]) | To("to") | Do(lambda: None)
    # It doesn't matter if you use the function directly or if you wrap it in Do :-)
    assert transition == Trigger("on") | From(["from", "from2"]) | To("to") | (lambda: None)
    s += transition
    s += transition
    s += transition
```
## License

This project is licensed under the GPL-3 license.
