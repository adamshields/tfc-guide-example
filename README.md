# Terraform Cloud Getting Started Guide Example

This is an example Terraform configuration intended for use with the [Terraform Cloud Getting Started Guide](https://learn.hashicorp.com/terraform/cloud-gettingstarted/tfc_overview).

## What will this do?

This is a Terraform configuration that will create an EC2 instance in your AWS account. 

When you set up a Workspace on Terraform Cloud, you can link to this repository. Terraform Cloud can then run `terraform plan` and `terraform apply` automatically when changes are pushed. For more information on how Terraform Cloud interacts with Version Control Systems, see [our VCS documentation](https://www.terraform.io/docs/cloud/run/ui.html).

## What are the prerequisites?

You must have an AWS account and provide your AWS Access Key ID and AWS Secret Access Key to Terraform Cloud. Terraform Cloud encrypts and stores variables using [Vault](https://www.vaultproject.io/). For more information on how to store variables in Terraform Cloud, see [our variable documentation](https://www.terraform.io/docs/cloud/workspaces/variables.html).

The values for `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` should be saved as environment variables on your workspace.


https://marketplace.visualstudio.com/_apis/public/gallery/publishers/HashiCorp/vsextensions/terraform/2.27.2023071109/vspackage?targetPlatform=win32-x64



https://marketplace.visualstudio.com/items?itemName=HashiCorp.terraform


Terraform Extension for Visual Studio Code
The HashiCorp Terraform Extension for Visual Studio Code (VS Code) with the Terraform Language Server adds editing features for Terraform files such as syntax highlighting, IntelliSense, code navigation, code formatting, module explorer and much more!

Quick Start
Get started writing Terraform configurations with VS Code in three steps:

Step 1: If you haven't done so already, install Terraform

Step 2: Install the Terraform Extension for VS Code.

Step 3: To activate the extension, open any folder or VS Code workspace containing Terraform files. Once activated, the Terraform language indicator will appear in the bottom right corner of the window.

New to Terraform? Read the Terraform Learning guides

See Usage for more detailed getting started information.

Read the Troubleshooting Guide for answers to common questions.

Features
IntelliSense Edit your code with auto-completion of providers, resource names, data sources, attributes and more
Syntax validation Diagnostics using terraform validate provide inline error checking
Syntax highlighting Highlighting syntax from Terraform 0.12 to 1.X
Code Navigation Navigate through your codebase with Go to Definition and Symbol support
Code Formatting Format your code with terraform fmt automatically
Code Snippets Shortcuts for common snippets like for_each and variable
Terraform Cloud Integration View Terraform Cloud Workspaces and Run details inside VS Code
Terraform Module Explorer View all modules and providers referenced in the currently open document.
Terraform commands Directly execute commands like terraform init or terraform plan from the VS Code Command Palette.
IntelliSense and Autocomplete
IntelliSense is a general term for a variety of code editing features including: code completion, parameter info, quick info, and member lists. IntelliSense features are sometimes called by other names such as autocomplete, code completion, and code hinting.

For Terraform constructs like resource and data, labels, blocks and attributes are auto completed both at the root of the document and inside other blocks. This also works for Terraform modules that are installed in the workspace, attributes and other constructs are autocompleted.

Note: If there are syntax errors present in the document upon opening, intellisense may not provide all completions. Please fix the errors and reload the document and intellisense will return. See hcl-lang#57 for more information.

Invoking intellisense is performed through the keyboard combination for your platform and the results depend on where the cursor is placed.

If the cursor is at the beginning of a line and no other characters are present, then a list of constructs like data, provider, resource, etc are shown.




















```
import subprocess
import pyperclip
import argparse
import os

def run_liquibase_command(command):
    """
    Run a Liquibase command and capture the output.
    """
    try:
        result = subprocess.run(command, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True, check=True)
        return result.stdout.decode('utf-8'), None
    except subprocess.CalledProcessError as e:
        return None, e.stderr.decode('utf-8')

def copy_to_clipboard(data):
    """
    Copy data to the clipboard.
    """
    pyperclip.copy(data)
    print("Output copied to clipboard.")

def save_to_file(data, filename):
    """
    Save data to a file.
    """
    with open(filename, 'w') as file:
        file.write(data)
    print(f"Output saved to {filename}")

def generate_script(base_filename, update_sql, rollback_sql):
    """
    Generate a script for the MySQL admin with both update and rollback SQL.
    """
    script_content = f"""-- Liquibase Update and Rollback SQL Script

-- Update SQL
-- To apply the update, run the following SQL commands:
{update_sql}

-- Rollback SQL
-- To rollback the update, run the following SQL commands:
{rollback_sql}
"""
    script_filename = f"{base_filename}_liquibase_script.sql"
    save_to_file(script_content, script_filename)
    print(f"Script generated: {script_filename}")

def main():
    parser = argparse.ArgumentParser(description='Run Liquibase commands and copy output to clipboard.')
    parser.add_argument('--liquibase-path', required=True, help='Path to Liquibase executable')
    parser.add_argument('--changelog-file', required=True, help='Path to Liquibase changelog file')
    parser.add_argument('--db-url', required=True, help='Database URL')
    parser.add_argument('--db-port', default='3306', help='Database port (default: 3306)')
    parser.add_argument('--db-username', default=os.getenv('DB_USERNAME'), help='Database username')
    parser.add_argument('--db-password', default=os.getenv('DB_PASSWORD'), help='Database password')
    parser.add_argument('--output-prefix', required=True, help='Prefix for output files')
    parser.add_argument('--jdbc-driver', required=True, help='Path to the JDBC driver JAR file')

    args = parser.parse_args()

    # Construct the JDBC URL with the port
    db_url_with_port = f"{args.db_url}:{args.db_port}"

    liquibase_classpath = f"{args.liquibase_path}/lib/{os.path.basename(args.jdbc_driver)}"

    update_sql_command = (
        f"{args.liquibase_path} --classpath={liquibase_classpath} --changeLogFile={args.changelog_file} "
        f"--url={db_url_with_port} --username={args.db_username} --password={args.db_password} updateSQL"
    )

    rollback_sql_command = (
        f"{args.liquibase_path} --classpath={liquibase_classpath} --changeLogFile={args.changelog_file} "
        f"--url={db_url_with_port} --username={args.db_username} --password={args.db_password} rollbackSQL"
    )

    print("Running Liquibase updateSQL...")
    update_sql_output, update_sql_error = run_liquibase_command(update_sql_command)
    if update_sql_output:
        update_filename = f"{args.output_prefix}_update.sql"
        save_to_file(update_sql_output, update_filename)
        copy_to_clipboard(update_sql_output)
    else:
        print(f"Error running updateSQL command: {update_sql_error}")

    print("Running Liquibase rollbackSQL...")
    rollback_sql_output, rollback_sql_error = run_liquibase_command(rollback_sql_command)
    if rollback_sql_output:
        rollback_filename = f"{args.output_prefix}_rollback.sql"
        save_to_file(rollback_sql_output, rollback_filename)
        copy_to_clipboard(rollback_sql_output)
    else:
        print(f"Error running rollbackSQL command: {rollback_sql_error}")

    if update_sql_output and rollback_sql_output:
        generate_script(args.output_prefix, update_sql_output, rollback_sql_output)

if __name__ == "__main__":
    main()

```
```
python script_name.py --liquibase-path /path/to/liquibase --changelog-file /path/to/changelog.xml --db-url jdbc:mysql://your_database_url --db-port 3306 --db-username your_db_username --db-password your_db_password --output-prefix my_liquibase_script --jdbc-driver /path/to/mysql-connector-java-X.X.X.jar


```


```
import subprocess
import pyperclip
import argparse
import os

def run_liquibase_command(command):
    """
    Run a Liquibase command and capture the output.
    """
    try:
        result = subprocess.run(command, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True, check=True)
        return result.stdout.decode('utf-8'), None
    except subprocess.CalledProcessError as e:
        return None, e.stderr.decode('utf-8')

def copy_to_clipboard(data):
    """
    Copy data to the clipboard.
    """
    pyperclip.copy(data)
    print("Output copied to clipboard.")

def save_to_file(data, filename):
    """
    Save data to a file.
    """
    with open(filename, 'w') as file:
        file.write(data)
    print(f"Output saved to {filename}")

def generate_script(base_filename, update_sql, rollback_sql):
    """
    Generate a script for the MySQL admin with both update and rollback SQL.
    """
    script_content = f"""-- Liquibase Update and Rollback SQL Script

-- Update SQL
-- To apply the update, run the following SQL commands:
{update_sql}

-- Rollback SQL
-- To rollback the update, run the following SQL commands:
{rollback_sql}
"""
    script_filename = f"{base_filename}_liquibase_script.sql"
    save_to_file(script_content, script_filename)
    print(f"Script generated: {script_filename}")

def main():
    parser = argparse.ArgumentParser(description='Run Liquibase commands and copy output to clipboard.')
    parser.add_argument('--liquibase-path', required=True, help='Path to Liquibase executable')
    parser.add_argument('--changelog-file', required=True, help='Path to Liquibase changelog file')
    parser.add_argument('--db-host', required=True, help='Database host')
    parser.add_argument('--db-port', default='3306', help='Database port (default: 3306)')
    parser.add_argument('--db-name', required=True, help='Database name')
    parser.add_argument('--db-username', default=os.getenv('DB_USERNAME'), help='Database username')
    parser.add_argument('--db-password', default=os.getenv('DB_PASSWORD'), help='Database password')
    parser.add_argument('--output-prefix', required=True, help='Prefix for output files')

    args = parser.parse_args()

    # Construct the JDBC URL with the host, port, and database name
    db_url = f"jdbc:mysql://{args.db_host}:{args.db_port}/{args.db_name}"

    # Hardcoded JDBC driver path
    jdbc_driver_path = "/path/to/mysql-connector-java-X.X.X.jar"  # Update this path to your JDBC driver location

    liquibase_classpath = f"{jdbc_driver_path}"

    update_sql_command = (
        f"{args.liquibase_path} --classpath={liquibase_classpath} --driver=com.mysql.cj.jdbc.Driver --changeLogFile={args.changelog_file} "
        f"--url={db_url} --username={args.db_username} --password={args.db_password} updateSQL"
    )

    rollback_sql_command = (
        f"{args.liquibase_path} --classpath={liquibase_classpath} --driver=com.mysql.cj.jdbc.Driver --changeLogFile={args.changelog_file} "
        f"--url={db_url} --username={args.db_username} --password={args.db_password} rollbackSQL"
    )

    print("Running Liquibase updateSQL...")
    update_sql_output, update_sql_error = run_liquibase_command(update_sql_command)
    if update_sql_output:
        update_filename = f"{args.output_prefix}_update.sql"
        save_to_file(update_sql_output, update_filename)
        copy_to_clipboard(update_sql_output)
    else:
        print(f"Error running updateSQL command: {update_sql_error}")

    print("Running Liquibase rollbackSQL...")
    rollback_sql_output, rollback_sql_error = run_liquibase_command(rollback_sql_command)
    if rollback_sql_output:
        rollback_filename = f"{args.output_prefix}_rollback.sql"
        save_to_file(rollback_sql_output, rollback_filename)
        copy_to_clipboard(rollback_sql_output)
    else:
        print(f"Error running rollbackSQL command: {rollback_sql_error}")

    if update_sql_output and rollback_sql_output:
        generate_script(args.output_prefix, update_sql_output, rollback_sql_output)

if __name__ == "__main__":
    main()


```






##########################################

```
import subprocess
import pyperclip
import argparse
import os

def run_liquibase_command(command):
    """
    Run a Liquibase command and capture the output.
    """
    try:
        result = subprocess.run(command, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True, check=True)
        return result.stdout.decode('utf-8'), None
    except subprocess.CalledProcessError as e:
        return None, e.stderr.decode('utf-8')

def copy_to_clipboard(data):
    """
    Copy data to the clipboard.
    """
    pyperclip.copy(data)
    print("Output copied to clipboard.")

def save_to_file(data, filename):
    """
    Save data to a file.
    """
    with open(filename, 'w') as file:
        file.write(data)
    print(f"Output saved to {filename}")

def generate_script(base_filename, update_sql, rollback_sql):
    """
    Generate a script for the MySQL admin with both update and rollback SQL.
    """
    script_content = f"""-- Liquibase Update and Rollback SQL Script

-- Update SQL
-- To apply the update, run the following SQL commands:
{update_sql}

-- Rollback SQL
-- To rollback the update, run the following SQL commands:
{rollback_sql}
"""
    script_filename = f"{base_filename}_liquibase_script.sql"
    save_to_file(script_content, script_filename)
    print(f"Script generated: {script_filename}")

def main():
    parser = argparse.ArgumentParser(description='Run Liquibase commands and copy output to clipboard.')
    parser.add_argument('--liquibase-path', required=True, help='Path to Liquibase executable')
    parser.add_argument('--changelog-file', required=True, help='Path to Liquibase changelog file')
    parser.add_argument('--db-host', required=True, help='Database host')
    parser.add_argument('--db-port', default='3306', help='Database port (default: 3306)')
    parser.add_argument('--db-name', required=True, help='Database name')
    parser.add_argument('--db-username', default=os.getenv('DB_USERNAME'), help='Database username')
    parser.add_argument('--db-password', default=os.getenv('DB_PASSWORD'), help='Database password')
    parser.add_argument('--output-prefix', required=True, help='Prefix for output files')

    args = parser.parse_args()

    # Construct the JDBC URL with the host, port, and database name
    db_url = f"jdbc:mysql://{args.db_host}:{args.db_port}/{args.db_name}"

    # Hardcoded JDBC driver path
    jdbc_driver_path = "/path/to/mysql-connector-java-X.X.X.jar"  # Update this path to your JDBC driver location

    liquibase_classpath = f"{jdbc_driver_path}"

    # Ensure the changelog file path is absolute
    changelog_file = os.path.abspath(args.changelog_file)

    update_sql_command = (
        f"{args.liquibase_path} --classpath={liquibase_classpath} --driver=com.mysql.cj.jdbc.Driver --changeLogFile={changelog_file} "
        f"--url={db_url} --username={args.db_username} --password={args.db_password} updateSQL"
    )

    rollback_sql_command = (
        f"{args.liquibase_path} --classpath={liquibase_classpath} --driver=com.mysql.cj.jdbc.Driver --changeLogFile={changelog_file} "
        f"--url={db_url} --username={args.db_username} --password={args.db_password} rollbackSQL"
    )

    print("Running Liquibase updateSQL...")
    update_sql_output, update_sql_error = run_liquibase_command(update_sql_command)
    if update_sql_output:
        update_filename = f"{args.output_prefix}_update.sql"
        save_to_file(update_sql_output, update_filename)
        copy_to_clipboard(update_sql_output)
    else:
        print(f"Error running updateSQL command: {update_sql_error}")

    print("Running Liquibase rollbackSQL...")
    rollback_sql_output, rollback_sql_error = run_liquibase_command(rollback_sql_command)
    if rollback_sql_output:
        rollback_filename = f"{args.output_prefix}_rollback.sql"
        save_to_file(rollback_sql_output, rollback_filename)
        copy_to_clipboard(rollback_sql_output)
    else:
        print(f"Error running rollbackSQL command: {rollback_sql_error}")

    if update_sql_output and rollback_sql_output:
        generate_script(args.output_prefix, update_sql_output, rollback_sql_output)

if __name__ == "__main__":
    main()
```






```
import os
import xml.etree.ElementTree as ET

# Function to create a new XML tree for a changelog
def create_changelog_tree():
    return ET.ElementTree(ET.Element('databaseChangeLog', {
        'xmlns': 'http://www.liquibase.org/xml/ns/dbchangelog',
        'xmlns:xsi': 'http://www.w3.org/2001/XMLSchema-instance',
        'xsi:schemaLocation': 'http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.8.xsd'
    }))

# Parse the generated changelog
tree = ET.parse('full_changelog.xml')
root = tree.getroot()

# Create a directory to store the individual changelogs
os.makedirs('changelogs', exist_ok=True)

# Dictionary to store table-specific changelogs
table_changelogs = {}

# Process each changeSet
for changeSet in root.findall('{http://www.liquibase.org/xml/ns/dbchangelog}changeSet'):
    # Identify table-related changes (e.g., createTable, addColumn)
    table_name = None
    if changeSet.find('{http://www.liquibase.org/xml/ns/dbchangelog}createTable') is not None:
        table_name = changeSet.find('{http://www.liquibase.org/xml/ns/dbchangelog}createTable').get('tableName')
    elif changeSet.find('{http://www.liquibase.org/xml/ns/dbchangelog}addColumn') is not None:
        table_name = changeSet.find('{http://www.liquibase.org/xml/ns/dbchangelog}addColumn').get('tableName')
    elif changeSet.find('{http://www.liquibase.org/xml/ns/dbchangelog}dropTable') is not None:
        table_name = changeSet.find('{http://www.liquibase.org/xml/ns/dbchangelog}dropTable').get('tableName')
    # Add more conditions if necessary for other table-related changes

    if table_name:
        if table_name not in table_changelogs:
            table_changelogs[table_name] = create_changelog_tree()
        table_changelogs[table_name].getroot().append(changeSet)

# Write each table-specific changelog to a file
for table_name, changelog_tree in table_changelogs.items():
    changelog_file = f'changelogs/{table_name}.xml'
    changelog_tree.write(changelog_file, xml_declaration=True, encoding='UTF-8')

# Create or update the master changelog to include individual changelogs
with open('db.changelog-master.xml', 'w') as master_file:
    master_file.write('''<databaseChangeLog
    xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.8.xsd">\n''')

    for table_name in table_changelogs.keys():
        master_file.write(f'    <include file="changelogs/{table_name}.xml"/>\n')

    master_file.write('</databaseChangeLog>')

```



```
import os
from lxml import etree as ET

# Function to create a new XML tree for a changelog
def create_changelog_tree():
    return ET.ElementTree(ET.Element('databaseChangeLog', nsmap={
        None: 'http://www.liquibase.org/xml/ns/dbchangelog',
        'xsi': 'http://www.w3.org/2001/XMLSchema-instance'
    }))

# Parse the generated changelog
tree = ET.parse('full_changelog.xml')
root = tree.getroot()

# Create a directory to store the individual changelogs
os.makedirs('changelogs', exist_ok=True)

# Dictionary to store table-specific changelogs
table_changelogs = {}

# Process each changeSet
for changeSet in root.findall('{http://www.liquibase.org/xml/ns/dbchangelog}changeSet'):
    # Identify table-related changes (e.g., createTable, addColumn)
    table_name = None
    if changeSet.find('{http://www.liquibase.org/xml/ns/dbchangelog}createTable') is not None:
        table_name = changeSet.find('{http://www.liquibase.org/xml/ns/dbchangelog}createTable').get('tableName')
    elif changeSet.find('{http://www.liquibase.org/xml/ns/dbchangelog}addColumn') is not None:
        table_name = changeSet.find('{http://www.liquibase.org/xml/ns/dbchangelog}addColumn').get('tableName')
    elif changeSet.find('{http://www.liquibase.org/xml/ns/dbchangelog}dropTable') is not None:
        table_name = changeSet.find('{http://www.liquibase.org/xml/ns/dbchangelog}dropTable').get('tableName')
    # Add more conditions if necessary for other table-related changes

    if table_name:
        if table_name not in table_changelogs:
            table_changelogs[table_name] = create_changelog_tree()
        table_changelogs[table_name].getroot().append(changeSet)

# Write each table-specific changelog to a file
for table_name, changelog_tree in table_changelogs.items():
    changelog_file = f'changelogs/{table_name}.xml'
    changelog_tree.write(changelog_file, xml_declaration=True, encoding='UTF-8', pretty_print=True)

# Create or update the master changelog to include individual changelogs
with open('db.changelog-master.xml', 'w') as master_file:
    master_file.write('''<databaseChangeLog
    xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.8.xsd">\n''')

    for table_name in table_changelogs.keys():
        master_file.write(f'    <include file="changelogs/{table_name}.xml"/>\n')

    master_file.write('</databaseChangeLog>')

```
