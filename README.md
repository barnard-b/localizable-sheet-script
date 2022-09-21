# localizable-sheet-script
A Google Sheets script that will take a sheet in a specific format and return iOS and Android localization files.

## What it does

For Android it creates an XML resources file with all of the strings. For iOS it creates a Localizable enum with String constants, and a .strings file. 

## Installing

1. Open your sheet.
2. Go to **Tools -> Script Editor**
3. Copy `Code.js`, make your edits if needed, and **Save**.

## Usage

1. Open your sheet.
2. Go to **Custom Export** and select your **iOS** or **Android**.

## Sheet format

The script expects the sheet to be formatted in a specific way.

| ... arbitrary number of columns before iOS keys | **Identifier iOS** | **Identifier Android** | English text | German text | ... |
|-------------------------------------------------|--------------------|------------------------|--------------|-------------|-----|
| place whatever you want in here                 | login_button_title | login_button_title     | Login        | Einloggen   |     |
|                                                 | ...                | ...                    | ...          | ...         |     |

**The texts in bold cannot be changed!** The script depends on them to know which identifier is which. The other texts don't matter.

The **first row** must **always** contain headers, and not the actual strings.

The number of languages depends on the `NUMBER_OF_LANGUAGES` variable in the script, and new languages can be added by adding a new column on the right and incrementing that number in the script.

The position of the first (iOS) column that is relevant to the script is changed with the `FIRST_COLUMN_POSITION` variable in the script. By default it's `1` (the first column).

## Configuring

 - `NUMBER_OF_LANGUAGES`: The number of language columns to use.
 - `FIRST_COLUMN_POSITION`: The position of the iOS identifiers (the first column relevant to the script). Starting from 1.
 - `IOS_INCLUDES_LOCALIZABLE_ENUM`: Whether or not to create an `Localizable` `enum` containing all of the keys as `static let` constants.
 
## Exported files

The exported files are the standard format (`strings.xml` or `Localizable.strings`) for the specific platforms. iOS also includes a `Localizable` `enum` which contains all of the keys as `static let` properties for code-completion and less typos. 
