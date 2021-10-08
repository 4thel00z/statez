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

### Synchronous example

```python
from statez import (
    Trigger,
    From,
    To,
    Do,
    StateMachine,
    Event
)

if __name__ == '__main__':
    s = StateMachine("HungryBoi", state="hungry")
    transition = Trigger("Eat") | From(["hungry", "dunno"]) | To("not_hungry") | Do(lambda a: True)
    # It doesn't matter if you use the function directly or if you wrap it in Do :-)
    assert transition == Trigger("Eat") | From(["hungry", "dunno"]) | To("not_hungry") | (lambda a: True)
    s += transition
    s.consume(Event("Eat"))
    assert s.state == "not_hungry", s.state
```

### Asynchronous example (Caution, this is dumb use of asyncio)

``` python
from statez import (
    Trigger,
    From,
    To,
    Do,
    AsyncStateMachine,
    Event,
)
import asyncio


async def return_bool(ignore):
    return True


if __name__ == "__main__":
    s = AsyncStateMachine("HungryBoi", state="hungry")
    transition = (
        Trigger("Eat") | From(["hungry", "dunno"]) | To("not_hungry") | Do(return_bool)
    )
    # It doesn't matter if you use the function directly or if you wrap it in Do :-)
    assert (
        transition
        == Trigger("Eat") | From(["hungry", "dunno"]) | To("not_hungry") | return_bool
    )
    s += transition
    asyncio.run(s.consume(Event("Eat")))
    assert s.state == "not_hungry", s.state
```

## License

This project is licensed under the GPL-3 license.
