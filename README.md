# debug_server
A utility to run two python programs in sync and check whether they produce identical numerical outputs.

The checked programs act as clients to the debug server.
Program executation is divided into check-points. In each check point, the clients 
send name/value pairs (string/numpy array) to the server and the server ensures
they are identical otherwise both clients start the debugger. In this case, 
Checkpoint data can be examined through local_data variable. Data sent by the other program
are stored in remote_data.

The server is started by running this script. Clients interact with the server
through the methods connect_to_server, send_data and check_point.

Checkpoint pass criteria can be changed by reimplementing _check_data function.
The current implementation assumes numerical or numpy array values and tests
them for (approximate) equality.

See _demo_client for an example of using the debug server.

# Demo
To test this script run these processes in seperate terminals:
   
```
python debug_test.py 
python debug_test.py --client
python debug_test.py --client
```
This results in the following output
![alt text](https://github.com/ahefnycmu/debug_server/blob/master/screenshot.png "Demo output")

# Additional Parameters
--server_ip: Specifies server ip [default 127.0.0.1].

--port: Specifies server port [default 6666].

--tol: Specifies error tolerance (measured in max absolute difference a.k.a $L_\infty$ error norm) [default 0.0].

--reuse: Sets SO_REUSEADDR socket option.

--single: Accepts a single client. No comparisons are made.

