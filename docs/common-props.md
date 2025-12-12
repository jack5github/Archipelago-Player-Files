# `name`

The name of the slot that one needs to log into in Archipelago. Limited to 16 characters.

- `{player}` will be replaced with the player's slot number.
- `{PLAYER}` will be replaced with the player's slot number, if that slot number is greater than 1.
- `{number}` will be replaced with the counter value of the name.
- `{NUMBER}` will be replaced with the counter value of the name, if the counter value is greater than 1.

# `description`

Used to describe a player file. Useful if you have multiple files. Use `|-` to allow the description to wrap across multiple lines.

# `game`

The name of the game that Archipelago is randomising.

# `requires` > `version`

The version of Archipelago required for a player file to work as expected.

# Game Options

Most game options consist of key-value pairs that represent the chance a given option will be enabled. By default, a single key-value pair is given a value of `50`, while all others are set to `0`. To make use of probabilities, change the values so they collectively add up to `100`.

## `progression_balancing`

A system that can move progression earlier, to try and prevent the player from getting stuck and bored early. A lower setting means more getting stuck. A higher setting means less getting stuck.

This property defaults to the following, which is the equivalent of `50`:

```yaml
random: 0
random-low: 0
random-high: 0
disabled: 0 # equivalent to 0
normal: 50 # equivalent to 50
extreme: 0 # equivalent to 99
```

To set it to a different value, set `normal` to 0 and create a new key/value pair like so: `<value>: 50`.

To set it to a random value, set `normal` to 0 and `random` to 50, then set `random-low` and `random-high` to the minimum and maximum values respectively.

## `accessibility`

Sets the rules for reachability of your items/locations.

- If `full` is enabled, everything can be reached and acquired.
- If `minimal` is enabled, only what is needed to reach your goal can be acquired.

# Item & Location Options

## `local_items`

A list of items that are forced to be in their native world.

## `non_local_items`

A list of items that are forced to be outside their native world.

## `start_inventory`

A dictionary of items and their quantity that the player starts with.

## `start_inventory_from_pool`

A dictionary of items and their quantity that the player starts with, but don't place them in the world. The game decides what the replacement items will be.

## `start_hints`

A list of items that are prefilled into the ``!hint`` command.

## `start_location_hints`

A list of locations (and their corresponding items) that are prefilled into the ``!hint`` command.

## `exclude_locations`

A list of locations that cannot have an important item.

## `priority_locations`

A list of locations that will always have an important item.

## `item_links`

A list of items that can be shared with other players.

## `plando_items`

Restrictions on where specific items can be found.
