# Data Quality Error Dictionary Guide

To simulate data quality errors, a dictionary structure is used where keys represent data fields to be modified, and the values are another dictionary detailing the transformations and the corresponding percentages of data to be affected.

Each inner dictionary comprises transformation function names as keys and a normalized percentage (between 0 and 1) as values. These percentages depict the proportion of the specific data field to undergo the given transformation.

### Important Note:
A given record can be subjected to multiple transformations for a particular field, so the sum of percentages can exceed 1. If you intend to apply the "null" transformation for a given field, ensure it's listed first. Once a field is set to NULL, subsequent transformations for that field are disregarded.

## General Transformations

These functions can be applied to any field in your dataset.

| Transformation      | Description                                               |
|---------------------|-----------------------------------------------------------|
| null                | Convert a value to NaN.                                   |
| only_first_char     | Retain only the first character of a value.               |
| none                | Convert a value to the string 'None'.                     |
| transpose           | Swap two consecutive characters.                          |
| delete_1char        | Remove a random character.                                |
| insert_1letter      | Introduce a random letter at a random position.           |
| insert_1num         | Insert a random number at a random position.              |
| repeat_1char        | Duplicate a random character.                             |
| leading_whitespace  | Add whitespace at the beginning.                          |
| trailing_whitespace | Append whitespace at the end.                             |

### DOB-Specific Transformations

| Transformation               | Description                                          |
|------------------------------|------------------------------------------------------|
| fake_date                    | Converts a value to a static date '2000-01-01'.     |
| dob_jan_first                | If the value has more than four characters, it changes the month and day to '01-01', keeping the original year. |
| year_equals_curyear          | Not provided in the initial data.                    |
| swap_month_day               | Switches the month and day values.                   |
| format_year_2digits          | Converts a 4-digit year to 2 digits.                 |
| format_slash_mdyyyy          | Format the date in 'MM/DD/YYYY' style.                   |

### Sex at Birth-Specific Transformations

| Transformation        | Description                                            |
|-----------------------|--------------------------------------------------------|
| other_O               | Converts a value to the string 'O'.                    |
| unknown_U             | Converts a value to the string 'U'.                    |
| oppositely_identify   | If the value is 'F', returns 'M'. If 'M', returns 'F'. Otherwise, returns the original value. |
| other                 | Converts a value to the string 'Other'.                |

### Address-Specific Transformations

| Transformation       | Description                                             |
|----------------------|---------------------------------------------------------|
| homeless             | Converts a value to the string 'Homeless'.              |
| longhand_compass     | Convert compass shorthand (e.g., 'N') to its longhand (e.g., 'North').   |
| longhand_roadtype    | Convert road type shorthand (e.g., 'St') to its longhand (e.g., 'Street').  |
| address_no_info      | Replace an address with a random value from a hand-crafted list of addresses with little-to-no information    |

### County Name-Specific Transformations

| Transformation | Description                                           |
|----------------|-------------------------------------------------------|
| no_county      | Removes ' County' from the value, if present.         |

### Zip/County FIPS-Specific Transformations

| Transformation               | Description                                   |
|------------------------------|-----------------------------------------------|
| format_remove_leading_zeros  | Removes leading zeros from a value.           |

### Phone-Specific Transformations

| Transformation            | Description                                    |
|---------------------------|------------------------------------------------|
| format_dash_only          | Formats the value with dashes only.            |
| format_parenthesis_dash   | Formats the value using parentheses and dashes.|
| prefix_plus1              | Adds a '+1' prefix to the value.               |

### Email-Specific Transformations

| Transformation    | Description                                        |
|-------------------|----------------------------------------------------|
| fake_email        |Replace email with a fake email address from a hand-crafted list  |
| no_provider       | Removes the domain provider from the email address.|


---

## Example Profiles

### 1. Simple Profile
The purpose of this example is to show you how easy it can be to introduce a few data quality issues into your dataset. Here, we're only making two potential changes to the `first_name` field:

- A small percentage of `first_name` entries might be set to `null`.
- A slightly larger percentage of `first_name` entries might have two of their characters transposed.

```python
simple_dataProfile = {
    'first_name':{
        'null': 0.05,
        'transpose': 0.1
    }
}
```

### 2. Complex Profile
This example is to demonstrate the depth and variety of transformations you can apply to each field. It gives a glimpse into how intricate and layered the data quality issues can be, mimicking real-world complexities:

- The `first_name` field has every general transformation applied to it.
- The `dob` field is modified by both general transformations and all dob-specific ones.
- The `phone` field is being transformed by all general and phone-specific methods. 

It's a comprehensive demonstration to show how granular and detailed you can get with these transformation profiles:

```python
complex_dataProfile = {
    'first_name': {
        'null': 0.05,
        'only_first_char': 0.03,
        'none': 0.02,
        'transpose': 0.04,
        'delete_1char': 0.03,
        'insert_1letter': 0.02,
        'insert_1num': 0.02,
        'repeat_1char': 0.03,
        'leading_whitespace': 0.02,
        'trailing_whitespace': 0.02
    },
    'dob': {
        'null': 0.05,
        'only_first_char': 0.02,
        'none': 0.01,
        'transpose': 0.03,
        'delete_1char': 0.03,
        'insert_1letter': 0.02,
        'insert_1num': 0.02,
        'repeat_1char': 0.03,
        'leading_whitespace': 0.02,
        'trailing_whitespace': 0.02,
        'fake_date': 0.04,
        'dob_jan_first': 0.04,
        'swap_month_day': 0.04,
        'format_year_2digits': 0.03,
        'format_slash_mdyyyy': 0.03
    },
    ...
    'phone': {
        'null': 0.05,
        'only_first_char': 0.02,
        'none': 0.01,
        'transpose': 0.03,
        'delete_1char': 0.03,
        'insert_1letter': 0.02,
        'insert_1num': 0.02,
        'repeat_1char': 0.03,
        'leading_whitespace': 0.02,
        'trailing_whitespace': 0.02,
        'format_dash_only': 0.03,
        'format_parenthesis_dash': 0.03,
        'prefix_plus1': 0.03
    }
}
```

These examples, especially the complex one, are meant to provide a thorough understanding of how to construct data quality profiles. Adjust the transformations and probabilities as required for your dataset.

---

### 3. Universal Data Profile

This example is to demonstrate the every possible transformation to apply to each field. 

```python

universal_dataProfile = {


    'first_name': {

        # General transformations
        'null': 0.0,
        'only_first_char': 0.0,
        'none': 0.0,
        'transpose': 0.0,
        'delete_1char': 0.0,
        'insert_1letter': 0.0,
        'insert_1num': 0.0,
        'repeat_1char': 0.0,
        'leading_whitespace': 0.0,
        'trailing_whitespace': 0.0

    },

    'middle_name': {

        # General transformations
        'null': 0.0,
        'only_first_char': 0.0,
        'none': 0.0,
        'transpose': 0.0,
        'delete_1char': 0.0,
        'insert_1letter': 0.0,
        'insert_1num': 0.0,
        'repeat_1char': 0.0,
        'leading_whitespace': 0.0,
        'trailing_whitespace': 0.0,

    },

    'last_name': {

        # General transformations
        'null': 0.0,
        'only_first_char': 0.0,
        'none': 0.0,
        'transpose': 0.0,
        'delete_1char': 0.0,
        'insert_1letter': 0.0,
        'insert_1num': 0.0,
        'repeat_1char': 0.0,
        'leading_whitespace': 0.0,
        'trailing_whitespace': 0.0

    },

    'dob': {

        # General transformations
        'null': 0.0,
        'only_first_char': 0.0,
        'none': 0.0,
        'transpose': 0.0,
        'delete_1char': 0.0,
        'insert_1letter': 0.0,
        'insert_1num': 0.0,
        'repeat_1char': 0.0,
        'leading_whitespace': 0.0,
        'trailing_whitespace': 0.0,

        # DOB-specific transformations
        'fake_date': 0.0,
        'dob_jan_first': 0.0,
        'year_equals_curyear': 0.0,
        'swap_month_day': 0.0,
        'format_year_2digits': 0.0,
        'format_slash_mdyyyy': 0.0

    },

    'sex_at_birth': {

        # General transformations
        'null': 0.0,
        'only_first_char': 0.0,
        'none': 0.0,
        'transpose': 0.0,
        'delete_1char': 0.0,
        'insert_1letter': 0.0,
        'insert_1num': 0.0,
        'repeat_1char': 0.0,
        'leading_whitespace': 0.0,
        'trailing_whitespace': 0.0,

        # Sex-specific transformations
        'other_O': 0.0,
        'unknown_U': 0.0,
        'oppositely_identify': 0.0,
        'other': 0.0

    },

    'address': {

        # General transformations
        'null': 0.0,
        'only_first_char': 0.0,
        'none': 0.0,
        'transpose': 0.0,
        'delete_1char': 0.0,
        'insert_1letter': 0.0,
        'insert_1num': 0.0,
        'repeat_1char': 0.0,
        'leading_whitespace': 0.0,
        'trailing_whitespace': 0.0,

        # Address-specific transformations
        'homeless': 0.0,
        'longhand_compass': 0.0,
        'longhand_roadtype': 0.0,
        'address_no_info': 0.0

    },

    'zip': {

        # General transformations
        'null': 0.0,
        'only_first_char': 0.0,
        'none': 0.0,
        'transpose': 0.0,
        'delete_1char': 0.0,
        'insert_1letter': 0.0,
        'insert_1num': 0.0,
        'repeat_1char': 0.0,
        'leading_whitespace': 0.0,
        'trailing_whitespace': 0.0,

        # ZIP-specific transformations
        'format_remove_leading_zeros': 0.0

    },

    'county_name': {

        # General transformations
        'null': 0.0,
        'only_first_char': 0.0,
        'none': 0.0,
        'transpose': 0.0,
        'delete_1char': 0.0,
        'insert_1letter': 0.0,
        'insert_1num': 0.0,
        'repeat_1char': 0.0,
        'leading_whitespace': 0.0,
        'trailing_whitespace': 0.0,

        # County-specific transformations   
        'no_county': 0.0

    },

    'city': {

        # General transformations
        'null': 0.0,
        'only_first_char': 0.0,
        'none': 0.0,
        'transpose': 0.0,
        'delete_1char': 0.0,
        'insert_1letter': 0.0,
        'insert_1num': 0.0,
        'repeat_1char': 0.0,
        'leading_whitespace': 0.0,
        'trailing_whitespace': 0.0

    },

    'state': {

        # General transformations
        'null': 0.0,
        'only_first_char': 0.0,
        'none': 0.0,
        'transpose': 0.0,
        'delete_1char': 0.0,
        'insert_1letter': 0.0,
        'insert_1num': 0.0,
        'repeat_1char': 0.0,
        'leading_whitespace': 0.0,
        'trailing_whitespace': 0.0

    },

    'phone': {

        # General transformations
        'null': 0.0,
        'only_first_char': 0.0,
        'none': 0.0,
        'transpose': 0.0,
        'delete_1char': 0.0,
        'insert_1letter': 0.0,
        'insert_1num': 0.0,
        'repeat_1char': 0.0,
        'leading_whitespace': 0.0,
        'trailing_whitespace': 0.0,

        # Phone-specific transformations
        'format_dash_only': 0.0,
        'format_parenthesis_dash': 0.0,
        'prefix_plus1': 0.0

    },

    'email': {

        # General transformations
        'null': 0.0,
        'only_first_char': 0.0,
        'none': 0.0,
        'transpose': 0.0,
        'delete_1char': 0.0,
        'insert_1letter': 0.0,
        'insert_1num': 0.0,
        'repeat_1char': 0.0,
        'leading_whitespace': 0.0,
        'trailing_whitespace': 0.0,

        # Email-specific transformations
        'fake_email': 0.0,
        'no_provider': 0.0
    }
}

```