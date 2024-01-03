# python
python.apitee.com


`PyYAML` library

```bash
pip install pyyaml
```

Python script that reads a YAML file and prints the `name`, `value`, and `items` for each entry. Here's an example script:

```python
import yaml

# Assuming the YAML structure is a list of dictionaries with the keys you mentioned
yaml_filename = 'example.yaml'

try:
    with open(yaml_filename, 'r') as yaml_file:
        data = yaml.safe_load(yaml_file)
        
        for entry in data:
            name = entry.get('name', 'N/A')  # Default to 'N/A' if 'name' is not found
            value = entry.get('value', 'N/A')  # Default to 'N/A' if 'value' is not found
            items = entry.get('items', 'N/A')  # Default to 'N/A' if 'items' is not found
            
            print(f"Name: {name}")
            print(f"Value: {value}")
            if isinstance(items, list):      # Check if 'items' is a list
                print("Items:")
                for item in items:
                    print(f" - {item}")
            else:
                print(f"Items: {items}")
            print('-------------')

except FileNotFoundError:
    print(f"The file {yaml_filename} does not exist.")
except yaml.YAMLError as exc:
    print(f"An error occurred while parsing the YAML file: {exc}")
```


In this script, we try to open the file `example.yaml` and parse its content with `yaml.safe_load()`. For each entry in the parsed data, we extract the `name`, `value`, and `items` keys and print their values.

Remember to change `example.yaml` to the actual YAML file you want to read.

Here's a simple example of what `example.yaml` could look like:

```yaml
- name: item1
  value: value1
  items:
    - subitem1
    - subitem2

- name: item2
  value: value2
  items:
    - subitem3
    - subitem4
```

Running the Python script with this YAML data will output the extracted `name`, `value`, and `items` fields, with `items` being listed if it's an array.
