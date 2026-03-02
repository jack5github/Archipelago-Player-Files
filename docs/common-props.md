# Common Properties

What follows are common properties that are found in Archipelago player files and descriptions of what they do. For more information, refer to [this Archipelago guide](https://archipelago.gg/tutorial/Archipelago/advanced_settings_en#root-options).

## `name`

The name of the slot that one needs to log into in Archipelago. Limited to 16 characters.

- `{player}` will be replaced with the player's slot number.
- `{PLAYER}` will be replaced with the player's slot number, if it is greater than 1.
- `{number}` will be replaced with the number of times the name is being used.
- `{NUMBER}` will be replaced with the number of times the name is being used, if it is greater than 1. (This is our preferred suffix in the case that we ever want to play multiple instances of the same game in a run.)

## `description`

Used to describe a player file. Useful if you have multiple files. Use `|-` to allow the description to wrap across multiple lines.

## `game`

The name of the game that Archipelago is randomising.

## `requires` > `version`

The version of Archipelago required for a player file to work as expected.

## Game Options

Most game options consist of key-value pairs that represent the chance a given option will be enabled. By default, a single key-value pair is given a value of `50`, while all others are set to `0`. To make use of probabilities, change the values so they collectively add up to `100`.

### `progression_balancing`

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

To set it to a different fixed value, set `normal` to 0 and create a new key/value pair like so: `<value>: 50`.

To set it to a random value, refer to the [RNG props guide](./rng-props.md).

### `accessibility`

Sets the rules for reachability of your items/locations.

- If `full` is enabled, everything can be reached and acquired.
- If `minimal` is enabled, only what is needed to reach your goal can be acquired.

## Item & Location Options

### `local_items`

A list of items that are forced to be in their native world.

### `non_local_items`

A list of items that are forced to be outside their native world.

### `start_inventory`

A dictionary of items and their quantity that the player starts with.

### `start_inventory_from_pool`

A dictionary of items and their quantity that the player starts with, but don't place them in the world. The game decides what the replacement items will be.

### `start_hints`

A list of items that are prefilled into the ``!hint`` command.

### `start_location_hints`

A list of locations (and their corresponding items) that are prefilled into the ``!hint`` command.

### `exclude_locations`

A list of locations that cannot have an important item.

### `priority_locations`

A list of locations that will always have an important item.

### `item_links`

A list of dictionaries which define items that are shared with other player files. Each dictionary in the list is defined as follows.

(For examples of how `item_links` is used, refer to the [Archipelago Advanced YAML Guide](https://archipelago.gg/tutorial/Archipelago/advanced_settings_en#example).)

- `name` - The name of the link. This should be a term that represents the items being shared (e.g. "Lasers", "Rods", etc.) but should not be too broad so as to overlap with an item or group name.
- `item_pool` - A list of item or group names from the player file's world that should be shared among other player files with the link.
- `local_items` - Item or group names from `item_pool` that are forced to be in the worlds of the player files with the link.
- `replacement_item` - The name of the item that will stand in for vacant slots created by sharing items, or `null` to have the generator randomly pick a filler item.
- `link_replacement` (optional) - A boolean where:
  - `true` - Will share replacement items among other player files with the link.
  - `false` - Will not share replacement items. (default)
- `skip_if_solo` (optional) - A boolean where:
  - `true` - Will cause the link to have no effect if there is only one player file with the link in the generation.
  - `false` - Will cause the link to always have an effect. (default)

`item_links` works irrespective of locations. This means that it is impossible to have specific locations in one player file give specific items to another player file. This option creates item-to-item relationships only.

### `plando_items`

A list of dictionaries which restrict where specific items can be found in the world. Each dictionary in the list is defined as follows.

(For examples of how `plando_items` is used, refer to the [Archipelago Plando Guide](https://archipelago.gg/tutorial/Archipelago/plando_en#item-plando-examples).)

#### Item Properties

- One of:
  - `items` - A dictionary of items that occupy the plando. The dictionary's keys are the item names, while the values are integers for a specific count of an item, or `true` for all of that item.
  - `item` - A dictionary of items that may occupy the plando, from which one is chosen. The dictionary's keys are the item names, while the values are integers for how likely the item is to be chosen proportional to the others specified.
- `count` (optional) - How many of the specified items to place in the plando. One of:
  - An integer - Places the specified number of items.
  - `false` - Places all specified item quantities. If not specified, items have a quantity of 1. (default)
  - A dictionary with the following optional keys:
    - `min` - The minimum quantity of items to place in the plando.
    - `max` - The maximum quantity of items to place in the plando.
- `from_pool` (optional) - A boolean where:
  - `true` - Will move the specified items from the item pool to the plando. (default)
  - `false` - Will created the specified items out of thin air, which may have unintended effects.

#### Location Properties

One of the following must be specified, or both.

- `world` - Which player file the plando is in. If this is specified, it is important to set `force` to `false` so that generation is possible if the specified world does not exist. One of:
  - The slot name of another player file.
  - A list of player file slot names.
  - `true` - Any player file except the current one.
  - `false` - The current player file. (default)
  - `null` - Any player file.
- One of:
  - `locations` - A list of location names that form the plando, in which the specified items can be found.
  - `location` - A single location name that forms the plando, in which the specified items can be found.
  - The above properties can include the strings `early_locations` (for checks found near the start of a run) or `non_early_locations` (for those found later).

#### Miscellaneous Properties

- `percentage` (optional) - An integer from 0 to 100 that specifies how likely the plando is to be enabled.
- `force` (optional) - A boolean or string where:
  - `true` - Halts the generation if the plando is impossible.
  - `false` - Ignores the plando if it is impossible and produce a warning.
  - `silent` - Ignores the plando if it is impossible with no warning. (default)
