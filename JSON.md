```markdown
# CAUTION: AI GENERATED CONTENT | NEEDS REVIEW

# JSON (JavaScript Object Notation)

JSON, which stands for [[JavaScript Object Notation]], is a light-weight data-interchange format that is easily readable and writeable by humans. It is based on a subset of the JavaScript Programming Language, Standard ECMA-262 3rd Edition - December 1999. Although it's derived from JavaScript, JSON is a language-independent data format. Code for parsing and generating JSON data is available in many programming languages.

## Characteristics

- **Lightweight**: JSON is considered lightweight because it requires minimal syntax to structure data.

- **Readable and writeable by humans**: JSON encodes data structures in a human-friendly format.

- **Language-independent**: While developed from JavaScript, JSON is a format that can be used independent of the language being used.

## Structure

JSON structures data as a collection of key-value pairs. These pairs can form complex structures by nesting data within other data. 

### Basic JSON Structure:

```json
{
  "key1": "value1",
  "key2": "value2",
  ...
}
```

Each key must be a string and is paired with a value, which could be various types: a string, number, object, array, or literals such as `null`, `true`, and `false`. Note that JSON does not support JavaScript's date object.

## Data Types

JSON supports the following data types:

- **Number**: A number in JSON could be integer, floating number, positive or negative. However, JSON does not support octal or hexadecimal formats.

- **String**: A string is a sequence of Unicode characters and is enclosed within double quotes. 

- **Boolean**: Represents either of two values: `true` or `false`. 

- **Array**: An array is an ordered collection of values. It's enclosed within square brackets `[]`, and the values are separated by a comma.

- **Object**: An object is an unordered collection of key-value pairs (also called properties). An object starts with left brace `{` and ends with right brace `}`.

- **null**: It represents an empty value.

## Use Cases

JSON is primarily used to transmit data between a [[server]] and a web [[application]], serving as an alternative to XML. It's also used in the configuration files of many software systems like package.json in [[Node.js]] or pom.xml in [[Java]].

```