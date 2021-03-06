#FAQ

#### 1. How to upgrade TDengine from 1.X versions to 2.X and above versions?

Version 2.X is a complete refactoring of the previous version, and configuration files and data files are incompatible. Be sure to do the following before upgrading:

1. Delete the configuration file, and execute <code>sudo rm -rf /etc/taos/taos</code>
2. Delete the log file, and execute <code>sudo rm -rf /var/log/taos </code>
3. ENSURE THAT YOUR DATAS ARE NO LONGER NEEDED! Delete the data file, and execute <code>sudo rm -rf /var/lib/taos </code>
4. Enjoy the latest stable version of TDengine
5. If the data needs to be migrated or the data file is corrupted, please contact the official technical support team for assistance

#### 2. When encoutered with the error "failed to connect to server", what can I do?

The client may encounter connection errors. Please follow the steps below for troubleshooting:

1. Make sure that the client and server version Numbers are exactly the same, and that the open source community and Enterprise versions are not mixed.
2. On the server side, execute `systemctl status taosd` to check the status of *taosd* service. If *taosd* is not running, start it and retry connecting.
3. Make sure you have used the correct server IP address to connect to.
4. Ping the server. If no response is received, check your network connection.
5. Check the firewall setting, make sure the TCP/UDP ports from 6030-6039 are enabled.
6. For JDBC, ODBC, Python, Go connections on Linux, make sure the native library *libtaos.so* are located at /usr/local/lib/taos, and /usr/local/lib/taos is in the *LD_LIBRARY_PATH*. 
7. For JDBC, ODBC, Python, Go connections on Windows, make sure *driver/c/taos.dll* is in the system search path (or you can copy taos.dll into *C:\Windows\System32*)
8. If the above steps can not help, try the network diagnostic tool *nc* to check if TCP/UDP port works
      check UDP port：`nc -vuz {hostIP} {port} `
      check TCP port on server:  `nc -l {port}`
      check TCP port on client: ` nc {hostIP} {port}`

#### 3. Why I get "Invalid SQL" error when a query is syntactically correct?

If you are sure your query has correct syntax, please check the length of the SQL string. Before version 2.0, it shall be less than 64KB. 

#### 4. Does TDengine support validation queries?

For the time being, TDengine does not have a specific set of validation queries. However, TDengine comes with a system monitoring database named 'sys', which can usually be used as a validation query object. 

#### 5. Can I delete or update a record that has been written into TDengine?

The answer is NO. The design of TDengine is based on the assumption that records are generated by the connected devices, you won't be allowed to change it. But TDengine provides a retention policy, the data records will be removed once their lifetime is passed.

#### 6. What is the most efficient way to write data to TDengine?

TDengine supports several different writing regimes. The most efficient way to write data to TDengine is to use batch inserting. For details on batch insertion syntax, please refer to [Taos SQL](../documentation/taos-sql)



