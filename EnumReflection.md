## EnumReflection

Over the years, questions about enumerations have regularly appeared on the forum, along with answers providing partial solutions:

- CommunityCommons offers a template (EnumerationFromString) that requires a customized Java version for each enum.
- There's module EnumToList. This module allows to transform an enumeration (as object attribute) into a list of object in order to iterate with a loop.
- ModelReflection contains enum data, but not all aspects are included.
- All enum information can be found in the MetaData. Unfortunately, in recent Mendix versions, this data is not available in the client (JavaScript).

So the (partly)solutions are scattered over a handfull of modules and require high-code alterations.
I searched for the most low-code solution possible and came up with the idea of EnumReflection.  


### How It Works

In an after start-up microflow (`ASU_EnumReflection`), the JavaAction `CreateMxObjectEnum` is executed. This JavaAction searches the MetaData and stores the found data in the entities `MxObjectEnum`, `MxObjectEnumValue`, and `MxObjectEnumCaption`.

These entities, attributes, and associations can be used directly—they are normal Mendix objects. Convenience microflows and nanoflows are also available to query this data. Additionally, there are Java and JavaScript Actions to modify enum values in an object. For those who want to view the data, there's a page called `Enumerations_Overview`.


### Query Functions


#### GetEnumValues

- **Parameter:**
  - `EnumName` - Full enum name (module.enumname like system.language)
- **Result:** List of `MxObjectEnumValue` with all values of the requested enum
- **Purpose:** To loop over all values of the enum. In the iteration, all data is available in the attributes of `MxObjectEnumValue`

#### GetEnumCaption

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
  - `LanguageCode` - In the format en_US, nl_NL
- **Result:** Caption associated with `EnumValue` and `LanguageCode`

#### GetEnumImageName

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
- **Result:** ImageName associated with `EnumValue`

#### GetEnumImage

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
  - `Enum_ImageEmbedding` - HTML or XML
- **Result:** Image associated with `EnumValue`

#### GetEnumImageURL

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
- **Result:** ImageURL associated with `EnumValue`

#### GetNextEnumValue

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
- **Result:** NextEnumValue or if no next value, empty string

#### GetNextMxObjectEnumValue (new in Ver. 1.2.0)

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
- **Result:** Next_MxObjectEnumValue or if no next value, empty object

#### GetPrevEnumValue
- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
- **Result:** PrevEnumValue or if no previous value, empty string

#### GetPrevMxObjectEnumValue (new in Ver. 1.2.0)

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
- **Result:** Prev_MxObjectEnumValue or if no previous value, empty object


### Enum Mutation Functions


#### NameToEnum

- **Parameters:**
  - `ObjectToChange` - MxObject
  - `AttributeName` - as string
  - `ValueAsString` - Key/Name as string
- **Result:** Attribute in Object receives the enum value corresponding to Value

#### CaptionToEnum

- **Parameters:**
  - `ObjectToChange` - MxObject
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `AttributeName` - as string
  - `ValueAsString` - Caption as string
- **Result:** Attribute in Object receives the enum value corresponding to Value

**Note:**
For the Enum Mutation Functions it is necessary to make a copy of the template function.
In the copied function you need to replace the placeholder entity (MxObject System.User) with the entity that has the enum to change as an attribute.
This is because the Mendix Modeler cannot handle abstract entities, but wants an explicit entity.
