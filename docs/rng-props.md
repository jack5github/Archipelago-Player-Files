What follows are all the random number generator-related properties that can be used to control the chosen value of a given property. For more information, refer to [this Archipelago guide](https://archipelago.gg/tutorial/Archipelago/advanced_settings_en#random-numbers).

# `random`

If selected by the given weights (the default is 50 for a single value, can be changed to be out of 100 for multiple values), chooses a random number between the minimum and the maximum for the given property. (This property is included in player templates by default.)

# `random-low`

Same as `random`, but the random number is more often a low number within the allowed range. (This property is included in player templates by default.)

# `random-middle`

Same as `random`, but the random number is more often a near-median number within the allowed range.

# `random-high`

Same as `random`, but the random number is more often a high number within the allowed range. (This property is included in player templates by default.)

# `random-range-#-#`

Same as `random`, but by replacing the hashes with a custom minimum and maximum, the range of the random number generator can be defined.

# `random-range-low-#-#`

Same as `random-range-#-#`, but the random number is more often a low number within the allowed range.

# `random-range-middle-#-#`

Same as `random-range-#-#`, but the random number is more often a near-median number within the allowed range.

# `random-range-high-#-#`

Same as `random-range-#-#`, but the random number is more often a high number within the allowed range.
