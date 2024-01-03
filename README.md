# python
python.apitee.com

## TODO:
- bash script with args
- install to /usr/bin
- start with file: apitee git.yaml
- start without file: apitee 
    - show list of files in current folder
    - show options:
        - generate script
        - update some SET VARIABLE, e.g. for testing purpose: apitee SET:MANAGER=apt
        - deploy on remote machine, e.g. apitee ENV:HOST:=212.221.22.3

```yaml
REQUIRE
    - 


SET_FROM_FILE:
    SSH:
        HOSTNAME: ./host/.name
        PASSWORD: ./host/.pass
        USERNAME: ./host/.user
        PORT: ./host/.port


SET:
    SSH: ssh {{PASSWORD}} {{USERNAME}}@{{HOSTNAME}}:{{PORT}}
    HOST:
        - cd {{NAME}}
        - SET_FROM_FILE SERVER
        - ssh {{PASSWORD}} {{USERNAME}}@{{HOSTNAME}}:{{PORT}}
    HOST:
        - cd {{NAME}}
        - SET_FROM_FILE:
            HOSTNAME: .name
            PASSWORD: .pass
            USERNAME: .user
            PORT: .port
        - ssh {{PASSWORD}} {{USERNAME}}@{{HOSTNAME}}:{{PORT}}

RUN:
    SSH:
        - whoami        
    HOST:
        client:
            - git clone https://github.com/apitee/python.git || bash
            - git clone https://github.com/apitee/examples.git
            - apitee example1
        server:
            - git clone https://github.com/apitee/python.git || bash
            - git clone https://github.com/apitee/examples.git
            - apitee example2
    FTP:
        webui:
            - git clone https://github.com/apitee/python.git || bash
            - git clone https://github.com/apitee/examples.git
```


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
