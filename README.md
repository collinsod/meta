# META
META is a toolbox for managing research data in MySQL databases. It comprises of four command line tools performing different tasks. The toolbox is cross-platform and can be build in Windows, Linux and Mac. 

## The toolbox
- 
###InitMETA
InitMETA initializes METAS's dictionary tables in a MySQL schema and generates the audit script files for both MySQL and snapshot file (SQLite).
#### *Parameters*
  - H - MySQL host server. Default is localhost
  - P - MySQL port. Default 3306
  - s - Schema to be initialized
  - u - User who has complete access to the schema
  - p - Password of the user
  - c - Create the dictionary tables. This will delete previous data including any audit records
  - d - Delete previous data
  - l - Load the dictionary data
  - v - Include views in the dictionary data
  - a - Target directory for the audit log script files

 ### *Example*
  ```sh
$ ./initmeta -u my_user -p my_pass -s my_schema -c -l -u ./my_audit_directory
```

- 
###MySQLToFile
MySQLToFile converts a MySQL schema (with META's dictionary tables) into common human readable formats like STATA, SPSS and CSV; and interoperable formats like XML, JSON and SQL.
#### *Parameters*
  - H - MySQL host server. Default is localhost
  - P - MySQL port. Default 3306
  - s - Schema to be converted
  - u - User who has select access to the schema
  - p - Password of the user
  - t - Table to be converted if only one table export is needed
  - d - Target directory for the export
  - o - Output format. For example STATA, SPSS, CSV, SQL, XML or JSON
  - n - Value to be used in case of NULL. Default is 0 (cero)
  - T - Include protected fields. In META you can define fields that contains sensitive data. By default MySQLToFile excluse such fields.

 ### *Example*
  ```sh
$ ./mysqltofile -u my_user -p my_pass -s my_schema -d ./my_target_directory -o STATA -n ""
```

- 
###GenSnapshot
GenSnapshot converts a MySQL schema (with META's dictionary tables) into a SQLite database (snapshot file) for off-line cleaning. The snapshot file records any changes in the data that later on could be synchronized against the MySQL server using *MySQLSync*.
#### *Parameters*
  - H - MySQL host server. Default is localhost
  - P - MySQL port. Default 3306
  - s - Schema to be converted
  - u - User who has select access to the schema
  - p - Password of the user
  - a - Input SQLite audit file created by InitMETA
  - o - Target SQLite file

 ### *Example*
  ```sh
$ ./gensnapshot -u my_user -p my_pass -s my_schema -a ./path_to_my_audit_file.sql -o my_snapshot_file.sqlite
```

- 
###MySQLSync
MySQLSync synchronizes the changes made in a snapshot file against the data in the MySQL server. It generates two files 1) an output file with warnings and errors occurring during the synchronization in CSV format, and 2) an script file containing any INSERT, DELETE or UPDATE performed in the server. 
#### *Parameters*
  - H - MySQL host server. Default is localhost
  - P - MySQL port. Default 3306
  - s - Schema to be converted
  - u - User who has select access to the schema
  - p - Password of the user
  - S - Input SQLite snapshot file
  - l - Output log file
  - o - Output SQL script file

 ### *Example*
  ```sh
$ ./mysqlsync -u my_user -p my_pass -s my_schema -S my_snapshot_file.sqlite -l path_to_my_log_file.CSV -o path_to_my_script_file.sql
```

## Technology
META was built using:

- [C++](https://isocpp.org/), a general-purpose programming language.
- [Qt 4](https://www.qt.io/), a cross-platform application framework.
- [TClap](http://tclap.sourceforge.net/), a small, flexible library that provides a simple interface for defining and accessing command line arguments.


## Building and testing
To build this site for local viewing or development:

    $ git clone https://github.com/ilri/meta.git
    $ cd meta
    $ qmake
    $ make

## Author
Carlos Quiros (c.f.quiros_at_cgiar.org / cquiros_at_qlands.com)

## License
This repository contains the code of:

- [TClap](http://tclap.sourceforge.net/) which is licensed under the [MIT license](https://raw.githubusercontent.com/twbs/bootstrap/master/LICENSE).


Otherwise, the contents of this application is [GPL V3](http://www.gnu.org/copyleft/gpl.html). 
