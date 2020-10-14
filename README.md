xxxx

ddd
This is a simple python tool to parse the unittest/pytest Result files then save the test suites and cases execution information to the Mysql database.

Database first
1. Create the database and tables in your instance of MySQL Server
Use provided /dal/create_db.sql to create the database in your instance of MySQL.

2. Use the 'sqlacodegen' tool in the virtual environment if the tables have updates to generate classes from an existing database.
# Template:
sqlacodegen --tables YOUR_TABLE --outfile src/dal/entities.p mysql+pymysql://USERNAME:PASSWORD@IP_ADDRESS_OF_MYSQL_SERVER:3306/DATABASE_NAME
# Example:
sqlacodegen --tables build_details --outfile src/dal/entities.py mysql+pymysql://superset:superset@localhost:3306/superset
How to use
1. Download or clone this repository
# clone repository:
git clone https://git@github.dxc.com:VPC-RnD/na-test-store.git
2. Create Python virtual environment and restore dependencies
python3 -m venv env

pip install -r requirements.txt
3. Activate Python virtual environment (Optional)
# Linux:
source env/bin/activate
# Windows:
env\Scripts\activate.bat
4. Configure the Connection String to your database
Edit the file /src/constants.py with the connection string to your MySQL instance:

connection_strings = "mysql+pymysql://USERNAME:PASSWORD@IP_ADDRESS_OF_MYSQL_SERVER:3306/DATABASE_NAME"
NB: the connection string depends on the connector we are using (PyMySQL), and SQLAlchemy itself.

5. Run
Run the file (python -m src.run -h) ...

usage: run.py [-h] folder_or_file_path job_name job_type {PYTEST,UNITTEST}

Automation testing framework arguments parser

positional arguments:
  folder_or_file_path   Test results path: pytest=json file path,
                        html=html file path,
                        jmeter=jmeter response.properties file path
                        unittest=xmlrunner folder path
  job_name              Job name
  job_type              Job type
  {PYTEST,UNITTEST,HTML,JMETER}
                        Parser Type

optional arguments:
  -h, --help            show this help message and exit
Example: python -m src.run C:/Users/cdiao2/test/PythonMySQL/xmlrunner api4firewall_DailyUT firewall UNITTEST
