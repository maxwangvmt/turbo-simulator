# turbo-simulator

[![Build Status](https://travis-ci.org/DongyiYang/turbo-simulator.svg?branch=master)](https://travis-ci.org/DongyiYang/turbo-simulator)

## What is turbo-simulator

Turbo-simulator is used to simulate Turbonomic server and test Turbonomic SDK probes.

## How does it work

Turbo-simulator builds a WebSocket connection with Turbonomic SDK probe/action-executor. It also exposes REST API for accepting user requests or configurations.

### Action Simulation
Action simulation can be used to test action execution of SDK probe/action-executor.

User can use REST API to create an action request, which simulates an action generated by ***Turbonomic Economic Scheduling Engine***. This API request is then be translated into a MediationServerMessage and sent to target probe via WebSocket communication. 

## How to build

Check out project to your *$GOPATH/src/github.com/turbonomic/* directory. Then

```console
$ make build
```

## How to use

First start turbo-simulator. Default address is *localhost* and port number is *1234*

```console
./turbo-simulator --v=3
```

Then configure probe to connect with turbo-simulator by providing the address and port number of turbo-simulator.

Current simulator only supports simulate action requests. An example move action request can be found as below:

```console
curl -X POST -H "Content-Type: application/json" http://localhost:1234/api/actions -d '{"type":"move","entityType":"Pod","entityID":"default:simple-server-b8kb2","moveSpec":{"destinationEntityType":"VirtualMachine","destinationIP":"1.2.3.4"}}'
```

More simulation functions will be added in the future. 
