# Contributing to ChipDB

You can contribute to ChipDB by updating/enhancing existing data, or by adding new parts definitions. Parts are specified using [YAML](http://yaml.org). (I chose YAML back in the day because it&apos;s more human-writable than JSON, and I typed in a *lot* of these things by hand.)

## File naming

One YAML file should represent one part, or a family of parts that all share a common pinout and roughly similar specifications. By convention, file names contain *only* uppercase letters, numbers, and hyphens `-`. If the properly-formatted part name contains lowercase letters or other characters (examples: ATmega328P, uPD7720), it can be specified with a `name` property (see below).

File contents should consist of 7-bit ASCII characters only. All special characters should be escaped with HTML entities.

## Definition syntax
At the root of the file should be a dictionary with the following fields:

#### `name`

Optional. Use if the properly-formatted part name is different from the filename. For example, `ATMEGA168.yaml` defines `name: ATmega168` because filenames should only include uppercase letters.

#### `description`

Required. A one-line description of the part, such as: `"8-bit shift register with 3-state output register"`.

#### `package`

Required.
This field was intended to indicate how the pin diagram of this part should be drawn.
The only value used in the original database was `DIP`.

#### `family`

Optional. If the part belongs to a large family, like the 7400 or 4000 series, it can be specified with this parameter. It is currently unused by ChipDB but could be used by other frontends to group parts by family. Currently defined families include `7400`, `4000`, `linear`, and `Atmel`.

#### `datasheet`

Required. The URL of an up-to-date version of the manufacturer&apos;s datasheet.

#### `aliases`

Optional. If similar parts share this pinout, you can specify an array of their names. For example, `ATMEGA168.yaml` defines `aliases: [ATmega48, ATmega88, ATmega328P]`. This *must* be an array, even if there is only one alias.

#### `pins`

Required.
An dictionary of pin definitions.
See the section "Pin definitions."

#### `specs`

Optional. An array of spec definitions. See the section "Spec definitions".

#### `notes`

Optional. An array of additional explanatory notes.


## Package definitions

Required.
Array of packages.
Packages contain a pin-mapping (array or dictionary).
For more detail see [packages.md](packages.md).


## Pin definitions

Each pin definition is a dictionary with a key and currently one field:

#### key

Required.
The pin symbol.
Typically all-uppercase.
In the case of a single-supply part, the supply pin should be `Vcc` and the ground pin should be `GND`.
Unused pins should be written as `NC` for "no connection" or "do not connect".
Not present pins should be written as `NOT_PRESENT` for missing leads.
May contain spaces, and subscript/overbar characters.
See "Subscripts and overbars."

#### `desc`

Required. Short description of the pin function. By convention, the first word is not capitalized. May contain subscript/overbar characters.


## Spec definitions

The `specs` array can be used to define a small table of basic specifications. Each definition is a dictionary with the following fields:

#### `param`

Required. Parameter name, such as `"Supply voltage"` or `"Slew rate"`.

#### `value`

Required. Parameter value. An array can be used to specify multiple values, like a minimum and maximum, e.g. `[8 (min), 36 (max)]`

#### `unit`

Optional. Parameter unit, like `V` or `mA`. Non-ASCII units should be written with HTML entities; e.g. `&Omega;` instead of &Omega;.


## Subscripts and overbars

ChipDB recognizes special syntax for overbars and subscripts in pin definitions, spec definitions, and notes.

#### Subscripts

If a sequence of non-whitespace characters is preceded by two underscores, it will be displayed as a subscript. Example: `D__0` becomes D<sub>0</sub>, `V__REF` becomes V<sub>REF</sub>.

#### Overbars

Tildes can be used to add overbars to characters. If a sequence of non-whitespace characters is preceded by a tilde, a line will be drawn above them. Example: `~OE` becomes <span style="text-decoration: overline;">OE</span>.

To add an overbar to a portion of a word, surround it with tildes. Example: `~RESET~/SYNC` becomes <span style="text-decoration: overline;">RESET</span>/SYNC, and `~CP~__0` becomes <span style="text-decoration: overline;">CP</span><sub>0</sub>

To include a literal tilde in the definition, use the HTML entity `&#126;`. If for some bizarre reason you want two or more literal underscores next to each other, use the HTML entity for underscore: `&#95;`.
