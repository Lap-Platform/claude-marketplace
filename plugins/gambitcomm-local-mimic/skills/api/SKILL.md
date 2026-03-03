---
name: mimic-rest-api
description: "MIMIC REST API skill. Use when working with MIMIC REST for mimic. Covers 356 endpoints."
version: 1.0.0
generator: lapsh
---

# MIMIC REST API
API version: 21.00

## Auth
Bearer basic

## Base URL
http://127.0.0.1

## Setup
1. Set Authorization header with your Bearer token
2. GET /mimic/get/max -- verify access
3. POST /mimic/agent/{agentNum}/add/{IP} -- create first add

## Endpoints

356 endpoints across 1 groups. See references/api-spec.lap for full details.

### mimic
| Method | Path | Description |
|--------|------|-------------|
| GET | /mimic/get/max | The maximum number of agent instances. |
| GET | /mimic/get/last | The last configured agent instance. |
| GET | /mimic/get/version | The version of the MIMIC command interface. |
| GET | /mimic/get/clients | The number of clients currently connected to the daemon. |
| GET | /mimic/get/cfgfile | The currently loaded lab configuration file for the particular user. |
| GET | /mimic/get/cfgfile_changed | This predicate indicates if the currently loaded agent configuration file has changed. |
| GET | /mimic/get/return | The return mode. |
| GET | /mimic/get/log | The current log file for the Simulator. |
| GET | /mimic/get/protocols | The set of protocols supported by the Simulator. |
| GET | /mimic/get/interfaces | The set of network interfaces that can be used for simulations. |
| GET | /mimic/get/product | The product number that is licensed. |
| GET | /mimic/get/netaddr | The network address of the host where the MIMIC simulator is running. |
| GET | /mimic/get/netdev | The default network device to be used for agent addresses. |
| GET | /mimic/get/configured_list | The list of {agentnum} that are currently configured. |
| GET | /mimic/get/active_list | The list of {agentnum} that are currently active (running or paused). |
| GET | /mimic/get/active_data_list | The list of {agentnum {statistics}} for agents that are currently active and whose statistics have changed since the last invocation of this command. |
| GET | /mimic/get/changed_config_list | The list of {agentnum} for which a configurable parameter changed. |
| GET | /mimic/get/changed_state_list | The list of {agentnum state} for which the state changed. |
| GET | /mimic/mget/{infoArray} | Get multiple sets of information about MIMIC, where infoArray is one of the parameters defined in the mimic get command. |
| PUT | /mimic/set/log | The current log file for the Simulator. |
| PUT | /mimic/set/netdev | The network address of the host where the MIMIC simulator is running. |
| PUT | /mimic/set/persistent | This operation flushes all global objects which need to be made persistent to disk. |
| PUT | /mimic/load/{cfgFile}/{firstAgentNum}/{lastAgentNum}/{startAgentNum} | Load the lab configuration file file. |
| PUT | /mimic/clear/{firstAgentNum}/{lastAgentNum} | Clear the lab configuration. |
| PUT | /mimic/saveas/{cfgFile}/{firstAgentNum}/{lastAgentNum} | Save the lab configuration in file. |
| PUT | /mimic/save | Save the lab configuration. |
| PUT | /mimic/start | Start MIMIC. |
| PUT | /mimic/stop | Stop MIMIC. |
| PUT | /mimic/terminate | Terminate the MIMIC daemon. |
| POST | /mimic/agent/{agentNum}/add/{IP} | Add an agent. |
| DELETE | /mimic/agent/{agentNum}/remove | Remove the current agent. |
| PUT | /mimic/agent/{agentNum}/start | Start the current agent. |
| PUT | /mimic/agent/{agentNum}/stop | Show the agent's primary IP address |
| PUT | /mimic/agent/{agentNum}/pause | Pause the current agent. |
| PUT | /mimic/agent/{agentNum}/halt | Halt the current agent. |
| PUT | /mimic/agent/{agentNum}/reload | Reload the current agent. |
| PUT | /mimic/agent/{agentNum}/resume | Resume the current agent. |
| GET | /mimic/agent/{agentNum}/get/interface | network interface card for the agent. |
| GET | /mimic/agent/{agentNum}/get/host | host address of the agent. |
| GET | /mimic/agent/{agentNum}/get/mask | subnet mask of the agent. |
| GET | /mimic/agent/{agentNum}/get/port | port number |
| GET | /mimic/agent/{agentNum}/get/protocol | protocols supported by agent |
| GET | /mimic/agent/{agentNum}/get/read | read community string |
| GET | /mimic/agent/{agentNum}/get/write | write community string |
| GET | /mimic/agent/{agentNum}/get/delay | one-way transit delay in msec. |
| GET | /mimic/agent/{agentNum}/get/start | relative start time |
| GET | /mimic/agent/{agentNum}/get/mibs | set of MIBs, simulations and scenarios |
| GET | /mimic/agent/{agentNum}/get/sim | first simulation name |
| GET | /mimic/agent/{agentNum}/get/scen | first scenario name |
| GET | /mimic/agent/{agentNum}/get/state | current running state of the agent |
| GET | /mimic/agent/{agentNum}/get/statistics | current statistics of the agent instance |
| GET | /mimic/agent/{agentNum}/get/changed | has the agent value space changed? |
| GET | /mimic/agent/{agentNum}/get/config_changed | has the lab configuration changed? |
| GET | /mimic/agent/{agentNum}/get/state_changed | has the agent state changed? |
| GET | /mimic/agent/{agentNum}/get/trace | SNMP PDU tracing |
| GET | /mimic/agent/{agentNum}/get/pdusize | maximum PDU size. |
| GET | /mimic/agent/{agentNum}/get/drops | drop rate (every N-th PDU). 0 means no drops. |
| GET | /mimic/agent/{agentNum}/get/owner | owner of the agent. |
| GET | /mimic/agent/{agentNum}/get/privdir | private directory of the agent. |
| GET | /mimic/agent/{agentNum}/get/oiddir | MIB directory of the agent. |
| GET | /mimic/agent/{agentNum}/get/validate | SNMP SET validation policy. |
| GET | /mimic/agent/{agentNum}/get/inform_timeout | timeout in seconds for retransmitting INFORM PDUs. |
| GET | /mimic/agent/{agentNum}/get/num_starts | number of starts for the agent. |
| PUT | /mimic/agent/{agentNum}/set/interface/{interface} | network interface card for the agent |
| PUT | /mimic/agent/{agentNum}/set/host/{host} | host address of the agent. |
| PUT | /mimic/agent/{agentNum}/set/mask/{mask} | subnet mask of the agent. |
| PUT | /mimic/agent/{agentNum}/set/port/{port} | port number |
| PUT | /mimic/agent/{agentNum}/set/protocol | protocols supported by agent as a comma-separated list |
| PUT | /mimic/agent/{agentNum}/set/read/{read} | read community string |
| PUT | /mimic/agent/{agentNum}/set/write/{write} | write community string |
| PUT | /mimic/agent/{agentNum}/set/delay/{delay} | one-way transit delay in msec |
| PUT | /mimic/agent/{agentNum}/set/start/{start} | relative start time |
| PUT | /mimic/agent/{agentNum}/set/mibs | set of MIBs, simulations and scenarios |
| PUT | /mimic/agent/{agentNum}/set/trace/{trace} | SNMP PDU tracing |
| PUT | /mimic/agent/{agentNum}/set/pdusize/{pdusize} | maximum PDU size |
| PUT | /mimic/agent/{agentNum}/set/drops/{drops} | drop rate (every N-th PDU) |
| PUT | /mimic/agent/{agentNum}/set/owner/{owner} | owner of the agent |
| PUT | /mimic/agent/{agentNum}/set/privdir/{privdir} | private directory of the agent. |
| PUT | /mimic/agent/{agentNum}/set/oiddir/{oiddir} | MIB directory of the agent. |
| PUT | /mimic/agent/{agentNum}/set/validate/{validate} | SNMP SET validation policy |
| PUT | /mimic/agent/{agentNum}/set/inform_timeout/{inform_timeout} | timeout in seconds for retransmitting INFORM PDUs |
| PUT | /mimic/agent/{agentNum}/save | Save agent MIB values. |
| GET | /mimic/agent/{agentNum}/ipalias/list | Lists all the additional ipaliases configured for the agent. |
| POST | /mimic/agent/{agentNum}/ipalias/add/{IP}/{port}/{mask}/{interface} | Adds a new ipalias for the agent. |
| DELETE | /mimic/agent/{agentNum}/ipalias/delete/{IP}/{port} | Deletes an existing ipalias from the agent. |
| PUT | /mimic/agent/{agentNum}/ipalias/start/{IP}/{port} | Starts an existing ipalias for the agent. |
| PUT | /mimic/agent/{agentNum}/ipalias/stop/{IP}/{port} | Stops an existing ipalias for the agent. |
| GET | /mimic/agent/{agentNum}/ipalias/status/{IP}/{port} | Returns the status (0=down, 1=up) of an existing ipalias for the agent. |
| GET | /mimic/agent/{agentNum}/trap/config/list | List the set of trap destinations for this agent instance. |
| POST | /mimic/agent/{agentNum}/trap/config/add/{IP}/{port} | Add a trap destination to the set of destinations. |
| DELETE | /mimic/agent/{agentNum}/trap/config/delete/{IP}/{port} | Remove a trap destination from the set of destinations. |
| GET | /mimic/agent/{agentNum}/trap/list | List the outstanding asynchronous traps for this agent instance. |
| GET | /mimic/agent/{agentNum}/from/list | List the source addresses that the agent will accept messages from. |
| POST | /mimic/agent/{agentNum}/from/add/{IP}/{port} | Add a source address that the agent will accept messages from. |
| DELETE | /mimic/agent/{agentNum}/from/delete/{IP}/{port} | delete a source address that the agent will accept messages from. |
| GET | /mimic/agent/{agentNum}/protocol/{prot}/get/config | Returns the protocol's configuration. |
| GET | /mimic/agent/{agentNum}/value/list/{OID} | Display the MIB objects below the current position |
| GET | /mimic/agent/{agentNum}/value/oid/{object} | Return the numeric OID of the specified object. |
| GET | /mimic/agent/{agentNum}/value/name/{OID} | Return the symbolic name of the specified object identifier. |
| GET | /mimic/agent/{agentNum}/value/mib/{object} | Return the MIB that defines the specified object. |
| GET | /mimic/agent/{agentNum}/value/info/{object} | Return the syntactical information for the specified object, such as type, size, range, enumerations, and ACCESS. |
| GET | /mimic/agent/{agentNum}/value/instances/{object} | Display the MIB object instances for the specified object. |
| GET | /mimic/agent/{agentNum}/value/eval/{object}/{instance} | Evaluate the values of the specified instance instance for each specified MIB object object and return it as it would through SNMP requests. |
| GET | /mimic/agent/{agentNum}/value/variables/{object}/{instance} | Display the variables for the specified instance instance for the specified MIB object object |
| GET | /mimic/agent/{agentNum}/value/split/{OID} | Split the numerical OID into the object OID and instance OID. |
| GET | /mimic/agent/{agentNum}/value/get/{object}/{instance}/{variable} | Get a variable in the Value Space. |
| PUT | /mimic/agent/{agentNum}/value/set/{object}/{instance}/{variable} | Set a variable in the Value Space. |
| GET | /mimic/agent/{agentNum}/value/meval/{objInsArray} | Evaluate the values of the specified instance instance for each specified MIB object object and return it as it would through SNMP requests. |
| PUT | /mimic/agent/{agentNum}/value/mset | Set multiple variables in the Value Space. |
| PUT | /mimic/agent/{agentNum}/value/munset | Unset multiple variables in the Value Space |
| GET | /mimic/agent/{agentNum}/value/mget/{objInsVarArray} | Get multiple variables in the Value Space. |
| PUT | /mimic/agent/{agentNum}/value/unset/{object}/{instance}/{variable} | Unset a variable in the Value Space in order to free its memory. |
| POST | /mimic/agent/{agentNum}/value/add/{object}/{instance} | Add an entry to a table. |
| DELETE | /mimic/agent/{agentNum}/value/remove/{object}/{instance} | Remove an entry from a table. |
| GET | /mimic/agent/{agentNum}/value/state/get/{object} | Get the state of a MIB object object. |
| PUT | /mimic/agent/{agentNum}/value/state/set/{object}/{state} | Set the state of a MIB object object |
| PUT | /mimic/store/set/{var}/{persist} | Set the variable store for the global storage |
| PUT | /mimic/agent/{agentNum}/store/set/{var}/{persist} | These commands allow the creation of a new variable, or changing an existing value. |
| PUT | /mimic/store/lreplace/{var}/{index} | These commands treat the variable as a list, and allow to replace an entry in the list at the specified index with the specified value. The variable has to already exist. |
| PUT | /mimic/agent/{agentNum}/store/lreplace/{var}/{index} | These commands treat the variable as a list, and allow to replace an entry in the list at the specified index with the specified value. The variable has to already exist. |
| PUT | /mimic/store/unset/{var} | Deletes a variable which is currently defined. |
| PUT | /mimic/agent/{agentNum}/store/unset/{var} | Deletes a variable which is currently defined. |
| GET | /mimic/store/get/{var} | Fetches the value associated with a variable. |
| GET | /mimic/agent/{agentNum}/store/get/{var} | Fetches the value associated with a variable. |
| GET | /mimic/store/exists/{var} | This command can be used as a predicate to ascertain the existence of a given variable. |
| GET | /mimic/agent/{agentNum}/store/exists/{var} | This command can be used as a predicate to ascertain the existence of a given variable. |
| GET | /mimic/store/persists/{var} | This command can be used as a predicate to ascertain the persistence of a given variable. |
| GET | /mimic/agent/{agentNum}/store/persists/{var} | This command can be used as a predicate to ascertain the persistence of a given variable. |
| GET | /mimic/store/list | This command will return the list of variables in the said scope. |
| GET | /mimic/agent/{agentNum}/store/list | This command will return the list of variables in the said scope. |
| PUT | /mimic/agent/{agentNum}/store/copy/{otherAgent} | This command copies the variable store from the other agent to this agent. |
| GET | /mimic/agent/{agentNum}/timer/script/list | List the timer scripts currently running along with the their intervals. |
| GET | /mimic/timer/script/list | List the timer scripts currently running along with the their intervals. |
| POST | /mimic/agent/{agentNum}/timer/script/add/{script}/{interval}/{arg} | Add a new timer script to be executed at specified interval (in msec) with the specified argument. |
| POST | /mimic/timer/script/add/{script}/{interval}/{arg} | Add a new timer script to be executed at specified interval (in msec) with the specified argument. |
| DELETE | /mimic/agent/{agentNum}/timer/script/delete/{script}/{interval}/{arg} | Remove a timer script from the execution list. |
| DELETE | /mimic/timer/script/delete/{script}/{interval}/{arg} | Remove a timer script from the execution list. |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmpv3/get/config | Returns the SNMPv3 configuration. |
| PUT | /mimic/agent/{agentNum}/protocol/msg/snmpv3/set/config/{parameter}/{value} | Changes the SNMPv3 configuration. |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmpv3/get/engineid | For started agents, retrieves the current engineID in use by the snmpv3 module. |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmpv3/get/engineboots | Retrieves the number of times the agent has been restarted. |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmpv3/get/enginetime | Retrieves the time in seconds for which the agent has been running. |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmpv3/get/context_engineid | Retrieves the contextEngineID for the agent instance. |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmpv3/user/list | Returns the current user entries as a Tcl list. |
| POST | /mimic/agent/{agentNum}/protocol/msg/snmpv3/user/add/{userName}/{securityName}/{authProtocol}/{authKey}/{privProtocol}/{privKey} | Adds a new user entry with the specified parameters. |
| DELETE | /mimic/agent/{agentNum}/protocol/msg/snmpv3/user/del/{userName} | Deletes the specified user entry. |
| DELETE | /mimic/agent/{agentNum}/protocol/msg/snmpv3/user/clear | Clears all user entries. |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmpv3/group/list | Returns the current group entries as an array of strings. |
| POST | /mimic/agent/{agentNum}/protocol/msg/snmpv3/group/add/{groupName}/{securityModel}/{securityName} | Adds a new group entry with the specified parameters. |
| DELETE | /mimic/agent/{agentNum}/protocol/msg/snmpv3/group/del/{groupName} | Deletes the specified group entry. |
| DELETE | /mimic/agent/{agentNum}/protocol/msg/snmpv3/group/clear | Clears all group entries. |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmpv3/access/list | Returns the current acccess entries as an array of strings. |
| POST | /mimic/agent/{agentNum}/protocol/msg/snmpv3/access/add/{groupName}/{prefix}/{securityModel}/{securityLevel}/{contextMatch}/{readView}/{writeView}/{notifyView} | Adds a new access entry with the specified parameters. |
| DELETE | /mimic/agent/{agentNum}/protocol/msg/snmpv3/access/del/{accessName} | Deletes the specified access entry. |
| DELETE | /mimic/agent/{agentNum}/protocol/msg/snmpv3/access/clear | Clears all access entries. |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmpv3/view/list | Returns the current view entries as an array of strings. |
| POST | /mimic/agent/{agentNum}/protocol/msg/snmpv3/view/add/{viewName}/{viewType}/{subtree}/{mask} | Adds a new view entry with the specified parameters. |
| DELETE | /mimic/agent/{agentNum}/protocol/msg/snmpv3/view/del/{viewName} | Deletes the specified view entry. |
| DELETE | /mimic/agent/{agentNum}/protocol/msg/snmpv3/view/clear | Clears all view entries. |
| PUT | /mimic/agent/{agentNum}/protocol/msg/snmpv3/usm/save | Saves current user settings in the currently loaded USM config file. |
| PUT | /mimic/agent/{agentNum}/protocol/msg/snmpv3/usm/saveas/{filename} | Saves current user settings in the specified USM config file. |
| PUT | /mimic/agent/{agentNum}/protocol/msg/snmpv3/vacm/save | Saves current group, access, view settings in the currently loaded VACM config file. |
| PUT | /mimic/agent/{agentNum}/protocol/msg/snmpv3/vacm/saveas/{filename} | Saves current group, access, view settings in the specified VACM config file. |
| GET | /mimic/agent/{agentNum}/protocol/msg/dhcp/get/args | Show the agent's DHCP argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/dhcp/get/config | Show the agent's DHCP configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/dhcp/set/config/{argument}/{value} | Set the agent's DHCP configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/dhcp/get/trace | Show the agent's DHCP traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/dhcp/set/trace/{enableOrNot} | Set the agent's DHCP traffic tracing |
| GET | /mimic/protocol/msg/dhcp/get/stats_hdr | Show the DHCP statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/dhcp/get/statistics | Show the agent's DHCP statistics |
| GET | /mimic/agent/{agentNum}/protocol/msg/dhcp/params | Show the parameters configured by the server in its DHCP-OFFER message |
| GET | /mimic/agent/{agentNum}/protocol/msg/tftp/get/args | Show the agent's TFTP argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/tftp/get/config | Show the agent's TFTP configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/tftp/set/config/{argument}/{value} | Set the agent's TFTP configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/tftp/get/trace | Show the agent's TFTP traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/tftp/set/trace/{enableOrNot} | Set the agent's TFTP traffic tracing |
| GET | /mimic/protocol/msg/tftp/get/stats_hdr | Show the TFTP statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/tftp/get/statistics | Show the agent's TFTP statistics |
| POST | /mimic/agent/{agentNum}/protocol/msg/tftp/session/read/server/{srcfile} | Create a read session to download srcfile from server |
| POST | /mimic/agent/{agentNum}/protocol/msg/tftp/session/write/server/{srcfile} | Create a read session to upload srcfile to server |
| GET | /mimic/agent/{agentNum}/protocol/msg/tftp/{sessionID}/get/{parameter} | Show a parameter of a TFTP sesssion |
| PUT | /mimic/agent/{agentNum}/protocol/msg/tftp/{sessionID}/set/{parameter}/{value} | Set a parameter of a TFTP sesssion |
| PUT | /mimic/agent/{agentNum}/protocol/msg/tftp/{sessionID}/start | Start a TFTP sesssion |
| GET | /mimic/agent/{agentNum}/protocol/msg/tftp/{sessionID}/status | Check a TFTP sesssion's status |
| PUT | /mimic/agent/{agentNum}/protocol/msg/tftp/{sessionID}/stop | Stop a TFTP sesssion |
| GET | /mimic/agent/{agentNum}/protocol/msg/tod/get/args | Show the agent's TOD argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/tod/get/config | Show the agent's TOD configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/tod/set/config/{argument}/{value} | Set the agent's TOD configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/tod/get/trace | Show the agent's TOD traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/tod/set/trace/{enableOrNot} | Set the agent's TOD traffic tracing |
| GET | /mimic/protocol/msg/tod/get/stats_hdr | Show the TOD statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/tod/get/statistics | Show the agent's TOD statistics |
| GET | /mimic/agent/{agentNum}/protocol/msg/tod/gettime/server/{serverAddr}/port/{portNum}/script/{scriptName}/timeout/{timeSec}/retries/{numRetries} | Retrieve TOD time |
| GET | /mimic/agent/{agentNum}/protocol/msg/telnet/get/args | Show the agent's TELNET argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/telnet/get/config | Show the agent's TELNET configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/telnet/set/config/{argument}/{value} | Set the agent's TELNET configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/telnet/get/trace | Show the agent's TELNET traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/telnet/set/trace/{enableOrNot} | Set the agent's TELNET traffic tracing |
| GET | /mimic/protocol/msg/telnet/get/stats_hdr | Show the TELNET statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/telnet/get/statistics | Show the agent's TELNET statistics |
| GET | /mimic/agent/{agentNum}/protocol/msg/telnet/server/get/state | Show the agent's TELNET server state |
| GET | /mimic/agent/{agentNum}/protocol/msg/telnet/server/get/rulesdb | Show the agent's TELNET rules db file name |
| GET | /mimic/agent/{agentNum}/protocol/msg/telnet/server/get/userdb | Show the agent's TELNET user db file name |
| GET | /mimic/agent/{agentNum}/protocol/msg/telnet/server/get/keymap | Show the agent's TELNET keymap file name |
| GET | /mimic/agent/{agentNum}/protocol/msg/telnet/server/get/users | Show the agent's TELNET users |
| GET | /mimic/agent/{agentNum}/protocol/msg/telnet/server/get/connections | Show the agent's TELNET connections |
| PUT | /mimic/agent/{agentNum}/protocol/msg/telnet/connection/logon/{connectionID}/{user}/{password} | Changes the connection's current logon. |
| PUT | /mimic/agent/{agentNum}/protocol/msg/telnet/connection/request/{connectionID}/{command} | Executes the command asynchronously . |
| PUT | /mimic/agent/{agentNum}/protocol/msg/telnet/connection/signal/{connectionID}/{signalName} | Triggers the asynchronous signal event with the specified signal name |
| PUT | /mimic/agent/{agentNum}/protocol/msg/telnet/ipalias/enable/{ipaddress}/{port} | Enable individual IP aliases on the agent and the simulator host |
| PUT | /mimic/agent/{agentNum}/protocol/msg/telnet/ipalias/disable/{ipaddress}/{port} | Disable individual IP aliases on the agent and the simulator host |
| GET | /mimic/agent/{agentNum}/protocol/msg/telnet/ipalias/isenabled/{ipaddress}/{port} | Check individual IP aliases on the agent and the simulator host |
| GET | /mimic/agent/{agentNum}/protocol/msg/telnet/ipalias/list | List all IP aliases on the agent and the simulator host |
| GET | /mimic/agent/{agentNum}/protocol/msg/ssh/get/args | Show the agent's SSH argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/ssh/get/config | Show the agent's SSH configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/ssh/set/config/{argument}/{value} | Set the agent's SSH configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/ssh/get/trace | Show the agent's SSH traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/ssh/set/trace/{enableOrNot} | Set the agent's SSH traffic tracing |
| GET | /mimic/protocol/msg/ssh/get/stats_hdr | Show the SSH statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/ssh/get/statistics | Show the agent's SSH statistics |
| PUT | /mimic/agent/{agentNum}/protocol/msg/ssh/ipalias/enable/{ipaddress}/{port} | Enable individual IP aliases on the agent and the simulator host |
| PUT | /mimic/agent/{agentNum}/protocol/msg/ssh/ipalias/disable/{ipaddress}/{port} | Disable individual IP aliases on the agent and the simulator host |
| GET | /mimic/agent/{agentNum}/protocol/msg/ssh/ipalias/isenabled/{ipaddress}/{port} | Check individual IP aliases on the agent and the simulator host |
| GET | /mimic/agent/{agentNum}/protocol/msg/ssh/ipalias/list | List all IP aliases on the agent and the simulator host |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmptcp/get/args | Show the agent's SNMPTCP argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmptcp/get/config | Show the agent's SNMPTCP configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/snmptcp/set/config/{argument}/{value} | Set the agent's SNMPTCP configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmptcp/get/trace | Show the agent's SNMPTCP traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/snmptcp/set/trace/{enableOrNot} | Set the agent's SNMPTCP traffic tracing |
| GET | /mimic/protocol/msg/snmptcp/get/stats_hdr | Show the SNMPTCP statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmptcp/get/statistics | Show the agent's SNMPTCP statistics |
| PUT | /mimic/agent/{agentNum}/protocol/msg/snmptcp/ipalias/enable/{ipaddress}/{port} | Enable individual IP aliases on the agent and the simulator host |
| PUT | /mimic/agent/{agentNum}/protocol/msg/snmptcp/ipalias/disable/{ipaddress}/{port} | Disable individual IP aliases on the agent and the simulator host |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmptcp/ipalias/isenabled/{ipaddress}/{port} | Check individual IP aliases on the agent and the simulator host |
| GET | /mimic/agent/{agentNum}/protocol/msg/snmptcp/ipalias/list | List all IP aliases on the agent and the simulator host |
| GET | /mimic/agent/{agentNum}/protocol/msg/syslog/get/args | Show the agent's SYSLOG argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/syslog/get/config | Show the agent's SYSLOG configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/syslog/set/config/{argument}/{value} | Set the agent's SYSLOG configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/syslog/get/trace | Show the agent's SYSLOG traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/syslog/set/trace/{enableOrNot} | Set the agent's SYSLOG traffic tracing |
| GET | /mimic/protocol/msg/syslog/get/stats_hdr | Show the SYSLOG statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/syslog/get/statistics | Show the agent's SYSLOG statistics |
| POST | /mimic/agent/{agentNum}/protocol/msg/syslog/send/{pri} | Set the agent's SYSLOG traffic tracing |
| GET | /mimic/agent/{agentNum}/protocol/msg/syslog/get/{attr} | Show the outgoing message's attributes |
| PUT | /mimic/agent/{agentNum}/protocol/msg/syslog/set/{attr}/{value} | Set the outgoing message's attributes |
| GET | /mimic/agent/{agentNum}/protocol/msg/ipmi/get/args | Show the agent's IPMI argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/ipmi/get/config | Show the agent's IPMI configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/ipmi/set/config/{argument}/{value} | Set the agent's IPMI configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/ipmi/get/trace | Show the agent's IPMI traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/ipmi/set/trace/{enableOrNot} | Set the agent's IPMI traffic tracing |
| GET | /mimic/protocol/msg/ipmi/get/stats_hdr | Show the IPMI statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/ipmi/get/statistics | Show the agent's IPMI statistics |
| GET | /mimic/agent/{agentNum}/protocol/msg/ipmi/get/{attr} | Show the outgoing message's attributes |
| PUT | /mimic/agent/{agentNum}/protocol/msg/ipmi/set/{attr}/{value} | Set the outgoing message's attributes |
| GET | /mimic/agent/{agentNum}/protocol/msg/proxy/get/args | Show the agent's PROXY argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/proxy/get/config | Show the agent's PROXY configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/proxy/set/config/{argument}/{value} | Set the agent's PROXY configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/proxy/get/trace | Show the agent's PROXY traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/proxy/set/trace/{enableOrNot} | Set the agent's PROXY traffic tracing |
| GET | /mimic/protocol/msg/proxy/get/stats_hdr | Show the PROXY statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/proxy/get/statistics | Show the agent's PROXY statistics |
| POST | /mimic/agent/{agentNum}/protocol/msg/proxy/port/add/{port}/{target}/{targetPort} | Add individual proxy target on the agent and the simulator host |
| DELETE | /mimic/agent/{agentNum}/protocol/msg/proxy/port/remove/{port} | Remove individual proxy target on the agent and the simulator host |
| GET | /mimic/agent/{agentNum}/protocol/msg/proxy/port/list | List all proxy targets |
| PUT | /mimic/agent/{agentNum}/protocol/msg/proxy/port/start/{port} | Start additional target |
| PUT | /mimic/agent/{agentNum}/protocol/msg/proxy/port/stop/{port} | Stop additional target |
| GET | /mimic/agent/{agentNum}/protocol/msg/proxy/port/isStarted/{port} | Check individual target |
| GET | /mimic/agent/{agentNum}/protocol/msg/netflow/get/args | Show the agent's NETFLOW argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/netflow/get/config | Show the agent's NETFLOW configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/netflow/set/config/{argument}/{value} | Set the agent's NETFLOW configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/netflow/get/trace | Show the agent's NETFLOW traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/netflow/set/trace/{enableOrNot} | Set the agent's NETFLOW traffic tracing |
| GET | /mimic/protocol/msg/netflow/get/stats_hdr | Show the NETFLOW statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/netflow/get/statistics | Show the agent's NETFLOW statistics |
| PUT | /mimic/agent/{agentNum}/protocol/msg/netflow/halt | Halt NETFLOW traffic |
| PUT | /mimic/agent/{agentNum}/protocol/msg/netflow/set/filename/{fileName} | Swap NETFLOW configuration file |
| PUT | /mimic/agent/{agentNum}/protocol/msg/netflow/set/collector/{collectorIP} | Swap NETFLOW collector |
| PUT | /mimic/agent/{agentNum}/protocol/msg/netflow/reload | Reload NETFLOW configuration before resuming traffic |
| PUT | /mimic/agent/{agentNum}/protocol/msg/netflow/resume | Resuming traffic |
| GET | /mimic/agent/{agentNum}/protocol/msg/netflow/flow/list | Show list of NETFLOW exports |
| PUT | /mimic/agent/{agentNum}/protocol/msg/netflow/flow/change/tfs_interval/{interval} | Change NETFLOW template export interval |
| PUT | /mimic/agent/{agentNum}/protocol/msg/netflow/flow/change/dfs_interval/{interval} | Change NETFLOW data export interval |
| PUT | /mimic/agent/{agentNum}/protocol/msg/netflow/flow/change/{flowset-uid}/{field-num}/{attr}/{value} | Change NETFLOW export attributes |
| GET | /mimic/agent/{agentNum}/protocol/msg/sflow/get/args | Show the agent's SFLOW argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/sflow/get/config | Show the agent's SFLOW configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/sflow/set/config/{argument}/{value} | Set the agent's SFLOW configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/sflow/get/trace | Show the agent's SFLOW traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/sflow/set/trace/{enableOrNot} | Set the agent's SFLOW traffic tracing |
| GET | /mimic/protocol/msg/sflow/get/stats_hdr | Show the SFLOW statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/sflow/get/statistics | Show the agent's SFLOW statistics |
| PUT | /mimic/agent/{agentNum}/protocol/msg/sflow/halt | Halt SFLOW traffic |
| PUT | /mimic/agent/{agentNum}/protocol/msg/sflow/reload | Reload SFLOW configuration before resuming traffic |
| PUT | /mimic/agent/{agentNum}/protocol/msg/sflow/resume | Resuming traffic |
| GET | /mimic/agent/{agentNum}/protocol/msg/web/get/args | Show the agent's WEB argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/web/get/config | Show the agent's WEB configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/web/set/config/{argument}/{value} | Set the agent's WEB configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/web/get/trace | Show the agent's WEB traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/web/set/trace/{enableOrNot} | Set the agent's WEB traffic tracing |
| GET | /mimic/protocol/msg/web/get/stats_hdr | Show the WEB statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/web/get/statistics | Show the agent's WEB statistics |
| GET | /mimic/agent/{agentNum}/protocol/msg/web/port/exists/{port} | Show the agent's WEB port |
| POST | /mimic/agent/{agentNum}/protocol/msg/web/port/add/{port} | Add the agent's WEB port |
| PUT | /mimic/agent/{agentNum}/protocol/msg/web/port/set/{port}/{protocol}/{version} | Set the agent's WEB port attribute |
| PUT | /mimic/agent/{agentNum}/protocol/msg/web/port/start/{port} | Start the agent's WEB port |
| PUT | /mimic/agent/{agentNum}/protocol/msg/web/port/stop/{port} | Stop the agent's WEB port |
| DELETE | /mimic/agent/{agentNum}/protocol/msg/web/port/remove/{port} | Remove the agent's WEB port |
| GET | /mimic/agent/{agentNum}/protocol/msg/mqtt/get/args | Show the agent's MQTT argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/mqtt/get/config | Show the agent's MQTT configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/set/config/{argument}/{value} | Set the agent's MQTT configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/mqtt/get/trace | Show the agent's MQTT traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/set/trace/{enableOrNot} | Set the agent's MQTT traffic tracing |
| GET | /mimic/protocol/msg/mqtt/get/stats_hdr | Show the MQTT statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/mqtt/get/statistics | Show the agent's MQTT statistics |
| GET | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/get/state | Show the agent's MQTT state |
| GET | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/get/protstate | Show the agent's MQTT TCP connection state |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/broker/{brokerAddr} | Set the agent's MQTT TCP connection target broker |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/port/{port} | Set the agent's MQTT TCP connection target port |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/clientid/{clientID} | Set the agent's MQTT client ID |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/username/{username} | Set the agent's MQTT client username |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/password/{password} | Set the agent's MQTT client password |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/willtopic/{topic} | Set the agent's MQTT client will's topic |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/willmsg/{msg} | Set the agent's MQTT client's will |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/willretain/{retain} | Set the agent's MQTT retained will |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/willqos/{qos} | Set the agent's MQTT will message's QOS field |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/cleansession/{cleanOrNot} | Set the agent's MQTT session |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/keepalive/{aliveTime} | Set the agent's MQTT TCP keepalive |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/on_disconnect/{action} | Set the agent's MQTT disconnection action |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/runtime/abort | Abort agent's MQTT TCP session without sending DISCONNECT command |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/runtime/disconnect | Disconnect agent's MQTT TCP session by sending DISCONNECT command |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/runtime/connect | Start agent's MQTT TCP session |
| GET | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/message/card | Show the agent's current messages' cardinality |
| GET | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/message/get/{msgNum}/{attr} | Show the agent's message attributes |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/message/set/{msgNum}/{attr}/{value} | Set the agent's message attributes |
| GET | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/subscribe/card | Show the agent's current subscriptions' cardinality |
| GET | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/subscribe/get/{subNum}/{attr} | Show the agent's subscription attributes |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/unsubscribe/{subNum} | Stops receiving messages from a subcription of the agent |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/resubscribe/{subNum} | Restart receiving messages from a subcription of the agent |
| PUT | /mimic/agent/{agentNum}/protocol/msg/mqtt/client/subscribe/set/{subNum}/{attr}/{value} | Set the agent's subscribe attributes |
| GET | /mimic/agent/{agentNum}/protocol/msg/coap/get/args | Show the agent's COAP argument structure |
| GET | /mimic/agent/{agentNum}/protocol/msg/coap/get/config | Show the agent's COAP configuration |
| PUT | /mimic/agent/{agentNum}/protocol/msg/coap/set/config/{argument}/{value} | Set the agent's COAP configuration |
| GET | /mimic/agent/{agentNum}/protocol/msg/coap/get/trace | Show the agent's COAP traffic tracing |
| PUT | /mimic/agent/{agentNum}/protocol/msg/coap/set/trace/{enableOrNot} | Set the agent's COAP traffic tracing |
| GET | /mimic/protocol/msg/coap/get/stats_hdr | Show the COAP statistics headers |
| GET | /mimic/agent/{agentNum}/protocol/msg/coap/get/statistics | Show the agent's COAP statistics |
| GET | /mimic/access/get/adminuser | Returns the current administrator. |
| GET | /mimic/access/get/admindir | Returns the current admin directory. |
| GET | /mimic/access/get/acldb | Returns the current access control database in use. |
| PUT | /mimic/access/set/acldb/{databaseName} | Allows setting the name of the current access control database. |
| GET | /mimic/access/get/enabled | Returns the state of access control checking. |
| PUT | /mimic/access/set/enabled/{enabledOrNot} | Allows the user to enable/disable the access control check. |
| PUT | /mimic/access/load/{filename} | Loads the specified file for access control data. |
| PUT | /mimic/access/save/{filename} | Saves current access control data in specified file. |
| GET | /mimic/access/list | Returns an array of entries. |
| POST | /mimic/access/add/{user}/{agents}/{mask} | Adds/Overwrites the user entry in the access control database. |
| DELETE | /mimic/access/del/{user} | Clears a users entry from access control database. |

## Enhanced Skill Content
## Question Mapping

- "How many agents can I run?" -> GET /mimic/get/max
- "Which agents are currently running?" -> GET /mimic/get/active_list
- "What is the current state of agent 5?" -> GET /mimic/agent/{agentNum}/get/state
- "How do I add a new SNMP agent at a specific IP?" -> POST /mimic/agent/{agentNum}/add/{IP}
- "How do I start all simulations at once?" -> PUT /mimic/start
- "What protocols does MIMIC support?" -> GET /mimic/get/protocols
- "How do I configure SNMPv3 users on an agent?" -> POST /mimic/agent/{agentNum}/protocol/msg/snmpv3/user/add/{userName}/{securityName}/{authProtocol}/{authKey}/{privProtocol}/{privKey}
- "What OID values does agent 3 expose?" -> GET /mimic/agent/{agentNum}/value/list/{OID}
- "How do I send a syslog message from an agent?" -> POST /mimic/agent/{agentNum}/protocol/msg/syslog/send/{pri}
- "How do I set up MQTT on an agent?" -> GET /mimic/agent/{agentNum}/protocol/msg/mqtt/get/config
- "What agents have unsaved configuration changes?" -> GET /mimic/get/changed_config_list
- "How do I create an IP alias for an agent?" -> POST /mimic/agent/{agentNum}/ipalias/add/{IP}/{port}/{mask}/{interface}
- "How do I configure trap destinations for an agent?" -> POST /mimic/agent/{agentNum}/trap/config/add/{IP}/{port}
- "How do I set up a NetFlow collector?" -> PUT /mimic/agent/{agentNum}/protocol/msg/netflow/set/collector/{collectorIP}
- "Who has access to manage agents?" -> GET /mimic/access/list

## Response Tips

- **System info endpoints** (`/mimic/get/*`): Return scalar values (strings, integers, or comma-separated lists). No pagination -- results are always complete.
- **Agent property getters** (`/mimic/agent/{agentNum}/get/*`): Return a single value per call. A 400 means the agent number is invalid or the agent is not configured.
- **List endpoints** (`*/list`): Return arrays of items (IP aliases, trap configs, users, timer scripts). No cursor-based pagination; all items return in one response.
- **Protocol config getters** (`*/get/config`): Return structured objects with named fields (see `@returns` schema per protocol). Fields vary by protocol type.
- **Statistics endpoints** (`*/get/statistics`): Return protocol-specific counters. Pair with `*/get/stats_hdr` to get column headers that label the statistics values.
- **Value space endpoints** (`*/value/*`): OID-centric responses; `eval` returns computed values, `variables` returns assignable fields, `meval`/`mget` support batch retrieval via array parameters.
- **Store endpoints** (`*/store/*`): Key-value responses. `exists` returns boolean, `persists` indicates persistence flag, `list` returns all variable names.

## Anomaly Flags

- **Agent state mismatch**: If `GET /mimic/agent/{agentNum}/get/state` returns an unexpected state after a start/stop/pause command, surface this immediately -- the agent may have hit a configuration error during transition.
- **Unsaved changes accumulating**: Proactively check `GET /mimic/get/changed_config_list` and `GET /mimic/get/changed_state_list` -- if these grow without `PUT /mimic/save` being called, warn about potential data loss on restart.
- **Config file drift**: If `GET /mimic/get/cfgfile_changed` returns true, flag that the running configuration differs from the saved file.
- **Agent 400 errors on valid numbers**: A 400 on a previously working agent number may indicate the agent was removed or the simulation was cleared -- check `GET /mimic/get/configured_list` to confirm.
- **SNMPv3 security gaps**: After adding users or groups via SNMPv3 endpoints, flag if USM/VACM databases have not been saved (`*/usm/save`, `*/vacm/save`) -- changes are lost on reload.
- **Protocol statistics anomalies**: If `*/get/statistics` shows high error counts or zero activity on a protocol that should be active, surface this as a potential misconfiguration.
- **MQTT disconnection loops**: If `*/mqtt/client/get/protstate` shows repeated disconnects after `connect`, flag the broker address, port, or credentials as likely misconfigured.
- **Trap destination unreachable**: After adding trap configs, if agent statistics show zero traps sent, flag the destination IP/port as potentially unreachable.

## Playbook

### 1. Set Up a New SNMP Agent from Scratch

1. Check available capacity: `GET /mimic/get/max` and `GET /mimic/get/configured_list`
2. Add the agent: `POST /mimic/agent/{agentNum}/add/{IP}`
3. Set the network interface: `PUT /mimic/agent/{agentNum}/set/interface/{interface}`
4. Set the subnet mask: `PUT /mimic/agent/{agentNum}/set/mask/{mask}`
5. Set the listening port: `PUT /mimic/agent/{agentNum}/set/port/{port}`
6. Load MIB files: `PUT /mimic/agent/{agentNum}/set/mibs`
7. Start the agent: `PUT /mimic/agent/{agentNum}/start`
8. Verify the state: `GET /mimic/agent/{agentNum}/get/state`
9. Save the configuration: `PUT /mimic/agent/{agentNum}/save`

### 2. Configure SNMPv3 Security on an Agent

1. Get current SNMPv3 config: `GET /mimic/agent/{agentNum}/protocol/msg/snmpv3/get/config`
2. Add a USM user: `POST /mimic/agent/{agentNum}/protocol/msg/snmpv3/user/add/{userName}/{securityName}/{authProtocol}/{authKey}/{privProtocol}/{privKey}`
3. Create a security group: `POST /mimic/agent/{agentNum}/protocol/msg/snmpv3/group/add/{groupName}/{securityModel}/{securityName}`
4. Define a view: `POST /mimic/agent/{agentNum}/protocol/msg/snmpv3/view/add/{viewName}/{viewType}/{subtree}/{mask}`
5. Set access rules: `POST /mimic/agent/{agentNum}/protocol/msg/snmpv3/access/add/{groupName}/{prefix}/{securityModel}/{securityLevel}/{contextMatch}/{readView}/{writeView}/{notifyView}`
6. Save USM database: `PUT /mimic/agent/{agentNum}/protocol/msg/snmpv3/usm/save`
7. Save VACM database: `PUT /mimic/agent/{agentNum}/protocol/msg/snmpv3/vacm/save`

### 3. Set Up NetFlow Export to a Collector

1. Get current NetFlow config: `GET /mimic/agent/{agentNum}/protocol/msg/netflow/get/config`
2. Set the flow data file: `PUT /mimic/agent/{agentNum}/protocol/msg/netflow/set/filename/{fileName}`
3. Set the collector address: `PUT /mimic/agent/{agentNum}/protocol/msg/netflow/set/collector/{collectorIP}`
4. Set the collector port: `PUT /mimic/agent/{agentNum}/protocol/msg/netflow/set/config/collectorport/{value}`
5. Reload the flow data: `PUT /mimic/agent/{agentNum}/protocol/msg/netflow/reload`
6. Resume exporting: `PUT /mimic/agent/{agentNum}/protocol/msg/netflow/resume`
7. Verify with statistics: `GET /mimic/agent/{agentNum}/protocol/msg/netflow/get/statistics`

### 4. Bulk Agent Management (Load, Start, Save)

1. Load agents from a config file: `PUT /mimic/load/{cfgFile}/{firstAgentNum}/{lastAgentNum}/{startAgentNum}`
2. Verify loaded agents: `GET /mimic/get/configured_list`
3. Start all agents at once: `PUT /mimic/start`
4. Confirm active agents: `GET /mimic/get/active_list`
5. When done, save all state: `PUT /mimic/save`
6. To archive a subset: `PUT /mimic/saveas/{cfgFile}/{firstAgentNum}/{lastAgentNum}`

### 5. Set Up an MQTT Client Simulation

1. Check MQTT config: `GET /mimic/agent/{agentNum}/protocol/msg/mqtt/get/config`
2. Set the broker: `PUT /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/broker/{brokerAddr}`
3. Set the port: `PUT /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/port/{port}`
4. Set client ID: `PUT /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/clientid/{clientID}`
5. Set credentials: `PUT /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/username/{username}` then `PUT .../set/password/{password}`
6. Set keepalive interval: `PUT /mimic/agent/{agentNum}/protocol/msg/mqtt/client/set/keepalive/{aliveTime}`
7. Connect to broker: `PUT /mimic/agent/{agentNum}/protocol/msg/mqtt/client/runtime/connect`
8. Verify connection state: `GET /mimic/agent/{agentNum}/protocol/msg/mqtt/client/get/protstate`
9. Check subscription count: `GET /mimic/agent/{agentNum}/protocol/msg/mqtt/client/subscribe/card`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
