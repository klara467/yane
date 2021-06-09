# Yet Another Network Emulator !?

Yes !

# Usage

## Basic usage

- Load and boot the network

   Creation of the multiple parts of the network (hosts, bridges,
links, ...)

```
$ yane [-s][-v]
```
  `-v` to run yane in verbose mode. ( to display logs performed via yanes start  )

  `-s <ID>` to give the session an ID. Must be unique.

 

  But what if you want to load and boot yane with your own config file ? No problem ! You can do it with :
```
$ yane -f <FILE_NAME>
```

- Sessions

   Multiple sessions can be run simultaneously. 
   To facilitate their use, the `-s` option should be used with each session's creation.
   A list of active sessions can be seen with :

```
$ yane -l
```
   A specific session can be killed with :
```
$ yane -s <SESSION_ID> -k
```
  The `-s` id option is not needed if a single session is running


  You can see the logs when you kill a session :
```
$ yane -v -s <SESSION_ID> -k
```
  Same as above, the `-s` id option is not needed if a single session is running


- Access 

  To link a host to current terminal :

```
$ yane -c <HOST_NAME>
```

  `-s` to specify which session to target
  `-c` to open a console on a specific host 

 
  If there is more than one session, we can specify the session wanted :

```
$ yane -s <SESSION_ID> -c <HOST_NAME>
```
 
  Last option but not least, you can open a forked terminal in a window on host with :
```
$ yane -s <SESSION_ID> -w <HOST_NAME>
```


You can always find help with :
```
$ yane -h
```

## Configuration and general structure

### Build your network :

  The network is described in a `yane.yml` file. This need to build different variables :

* host

  list of host name and mode

  ```yaml
  hosts:
    name: NAME
    mode: docker | netns
  ```

* BridgeInterface :

  bridgeInterfaces is an array (indexed by bridge names) of BridgeInterface

   ! separated list of interface list

   **Example :**
  ```yaml
  bridges:
    name: myBr
    mode: switched
    interfaces: host-a:v0!host-b:v0!host-c:v0
  ```
* Point to point link

   `i1!i2`

   where

   i1 is one interface

   i2 is another interface

   **Example :**
  ```yaml
  links:
    - host-a:v0:192.168.1.1/24!host-b:v0:192.168.1.2/24
  ```
* Interface

   As you can see above interfaces are always described with :
   ```
   h:i[:A]
   ```

  where

     `h` is the host

     `i` os the interface name within the host

     `a` is an IPv4 address

  **Example :**
  ```
  host-a:v0:192.168.10.2/24
  ```
