# Scan Monitor Dashboard Setup

## I. Steps to Deploy Seele Monitor

### 1.	Install Required Tools
#### 1）	Install Node
```bash
yum install node
```
#### 2）	Install pm2
```bash
yum install pm2
```
#### 3）	Install nginx
```bash
yum install nginx
```
### 2.	Deploy a Monitor
#### 1)	Download the monitor source code
```bash
git clone https://github.com/seeleteam/monitor
```
#### 2） Modify the frontend service config of the monitor
In `config/dev.env.js`, modify the development environment config:
```bash
NODE_ENV: '"development"',  // dev mode
BOWER_SERVER: '"ws://x.x.x.x:3000/bower"', // monitor backend websocket server
BOWER_CLIENT_HEARTCHECK_TIMEOUT: 5000, // monitor vue client heartcheck timeout
BOWER_CLIENT_RECONNECT_TIMEOUT: 5000 // monitor vue client reconnect timeout
```
In `config/prod.env.js`, modify the production environment config:
```bash
NODE_ENV: '"production"',  // prod mode
BOWER_SERVER: '"ws://x.x.x.x:3000/bower"', // monitor backend websocket server
BOWER_CLIENT_HEARTCHECK_TIMEOUT: 5000, // monitor vue client heartcheck timeout
BOWER_CLIENT_RECONNECT_TIMEOUT: 5000 // monitor vue client reconnect timeout
```
#### 3） Modify the monitor websocket services configuration
Modify the file `config/process.json`:
```bash
{
    "apps" : [
      {
        "name" : "monitor_server", // monitor backend server name
        "script" : "server/app.js", // monitor backend server entry script
        "watch": ["server"], 
        "interpreter": "node", // monitor backend server start command
        "env": {
          "NODE_ENV": "development",
          "SERVER_NGINX": 0, // monitor backend deploy to nginx flag
          "WS_CLIENT_CONN_TIMEOUT": 15, // check monitor client offline timeout
          "WS_CLIENT_CONN_INTERVAL": 30000, // check all monitor client offline interval
          "SERVER_PORT": 3000, // monitor backend port
          "BOWER_SERVER_DATA_UPDATE_INTERVAL": 5000, // monitor backend data update interval
"NODE_SHARD": 1 //seele node shard num
        },
        "env_production" : {
          "NODE_ENV": "production",
          "SERVER_NGINX": 1,
          "WS_CLIENT_CONN_TIMEOUT": 15,
          "WS_CLIENT_CONN_INTERVAL": 30000,
          "SERVER_PORT": 3000,
          "BOWER_SERVER_DATA_UPDATE_INTERVAL": 5000,
"NODE_SHARD": 1
        }
      }
    ]
}
```
#### 4）	Install and Compile the Code
``` bash
cd monitor
npm install
npm run build
```
#### 5) Start the Monitor Websocket Service
##### Development Environment：
``` bash   
cd monitor
pm2 start config/process.json --env development
```   
##### Production Environment：
```bash   
cd monitor
pm2 start config/process.json --env production
```
#### 6) Start the Monitor Front Service:
##### Development Environment：
```bash
cd ./monitor
npm run dev
```   
##### Production Environment：
```bash
nginx config file conf.d/monitor.conf
   server {
        listen      3001;
        server_name  _;
        root         /usr/local/nginx/monitor01;
        location / {
            index  index.html index.htm;
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }
cp -r ./monitor/dist  /usr/local/nginx/monitor01
nginx -s reload
```
### 3.	Deploy the monitor-frame
#### 1)	Download the monitor-frame Source Code
```bash
git clone https://github.com/seeleteam/monitor-frame
```
#### 2） Modify the monitor-frame Config
Modify the file `src/pages/url.js`:
```bash
  // set the shard view of seele-monitor, default display index 1
  menuList: [
    {
      id: '1', // index unique id
      menuName: 'Shard 01', // display name
      url: 'http://localhost:3001' // access url
    },
  ]
```  
#### 3）Install and Compile the Code
```bash
cd monitor-frame
npm install
npm run build
```
#### 4) Start the monitor-frame
##### Development Environment
```bash   
cd ./monitor-frame
npm run dev
```
##### Production Environment
```bash
nginx config file conf.d/monitor-frame.conf
   server {
        listen      8000;
        server_name  _;
        root         /usr/local/nginx/monitor-frame;
        location / {
            index  index.html index.htm;
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }
cp -r ./monitor-frame/dist  /usr/local/nginx/monitor-frame
nginx -s reload
```
### 4.	Deploy monitor-api
#### 1)	Download monitor-api Source Code 
```bash
git clone https://github.com/seeleteam/monitor-api
```
#### 2)	Compile monitor-api
```bash
cd monitor-api
make
```
#### 3)	Edit monitor-api Configurations
Edit the config file `config/app.conf`
```bash
app_name = monitor-api   // monitor api name
addr = :9997             // default monitor-api server port
run_mode = dev          // select run mode
DisableConsoleColor = true
MonitorConfigFile = ./config/monitor.json
# comment should be above the line
[dev]
# http server address, format ip:port
addr = :9997           // monitor-api server port
LimitConnection = 0
# enable web socket
EnableWebSocket = true
# enable rpc
EnableRPC = true
DisableConsoleColor = false

# enable write log out
WriteLog = true

# web socket api
WsRouter = /api

# every 10s send the node info to monitor server
WsFullEventTickerTime = 10
# every 2s send the block info, if the block height changed
WsLatestBlockEventTickerTime = 2
# if web socket occur error, reconnect delay 5s
DelayReConnTime = 5
# if rpc occur error, reconnetct and resend delay 5s
DelaySendTime = 5
# if rpc server occur error over 10, report error to monitor server
ReportErrorAfterTimes = 10
# RPC server addr for go-seele node, format ip:port
RPCURL = 127.0.0.1:55027   // seele node rpc
# log level, debug, info, warn, error, fatal, panic
LogLevel = debug

[prod]
addr = :9997
EnableWebSocket = true
EnableRPC = true
WriteLog = true
LogFile = monitor-api.log
MonitorConfigFile = ./config/monitor.json
WsRouter = /api
WsFullEventTickerTime = 10
WsLatestBlockEventTickerTime = 2
DelayReConnTime = 5
DelaySendTime = 4
RPCUrl = 127.0.0.1:55027      // seele node rpc
# debug, info, warn, error, fatal, panic
LogLevel = info
```
Edit the config file `config/monitor.conf`
```bash
{
    "1":"x.x.x.x:3001",  // shard1 monitor websocket url
    "2":"x.x.x.x:3001",  // shard2 monitor websocket url
    "3":"x.x.x.x:3001"  // shard3 monitor websocket url
}
```
#### 4)	Start monitor-api
```bash
./monitor-api start -c config.conf
```
#### 5) In your Browser, visit the monitor http://localhost:3001

## II. Steps to Deploy Seele scan

### 1.Install Required Tools
  - Install [go](https://golang.org/dl/) v1.7 or higher and the [C compiler](https://gcc.gnu.org/). 
  - Install [mongodb](https://www.mongodb.com/download-center) version 3.63 or higher

### 2.Deploy Seele Data Synchronization Nodes
  - Download and compile [go-seele](Getting-Started-With-Seele.html)
  - Start a go-seele node, ensure that the node is p2p connected with other go-seele nodes, and run:
  
```bash
  ./seele-node1 start -c config/node1.json --accounts config/accounts.json --miner stop
```
### 3. Deploy scan-api
#### 1）Download and compile scan-api
  - Download scan-api source code to [GOPATH](https://github.com/golang/go/wiki/SettingGOPATH) `src\github.com` directory
```bash
git clone https://github.com/seeleteam/scan-api
```  
  - In `seeleteam\scan-api`, compile scan-api, which will create seele_syncer, scan_server, chart_service, and node_service, 4 executable programs within `scan-api\build\`。
```bash
cd seeleteam/scan-api
make
```

#### 2）Modify scan-api Service Configurations
##### seele_syncer Configurations：
<a name="seele_syncer">

	{
		"RpcURL": "0.0.0.0:55026",
		"WriteLog": true,
		"LogLevel": "debug",
		"LogFile": "seele-syncer.log",
		"DataBaseConnUrl":"127.0.0.1:27017",
		"DataBaseName":"seele",
		"SyncInterval":3,
		"ShardNumber": 2
	}
</a>
<table>  <tbody>
<tr>
<th>Service</th>
<th>Parameter</th>
<th>Explanation</th>
</tr>
<tr>
<th rowspan="8">seele_syncer</th>
<td>RpcURL</td>
<td>seele node's rpc connection address</td>
</tr>
<tr>
<td>WriteLog</td>
<td>switch for log read/write</td>
</tr>
<tr>
<td>LogLevel</td>
<td>Level of log</td>
</tr>
<tr>
<td>LogFile</td>
<td>Filename of log</td>
</tr>
<tr>
<td>DataBaseConnUrl</td>
<td>mongodb connection address</td>
</tr>
<tr>
<td>DataBaseName</td>
<td>Database name of mongodb</td>
</tr>
<tr>
<td>SyncInterval</td>
<td>seele-node rpc sync time interval</td>
</tr>
<tr>
<td>ShardNumber</td>
<td>Shard ID</td>
</tr>
</table>

#### scan_server Configurations：
<a name="scan_server">

	{
		"GinMode":"debug",
		"Addr": ":8888", 
		"WriteLog": true,
		"LogLevel": "debug",
		"LogFile": "scan-api.log",
		"DataBaseConnUrl":"127.0.0.1:27017",
		"DataBaseName":"seele"
	}
</a>
<table> <tbody>
<tr>
<th>Service</th>
<th>Paramater</th>
<th>Explanation</th>
</tr>
<tr>
<th rowspan="8">scan_server</th>
<td>GinMode</td>
<td>Mode of operation for Gin</td>
</tr>
<tr>
<td>Addr</td>
<td>Service listening port</td>
</tr>
<tr>
<tr>
<td>WriteLog</td>
<td>Switch for log read/write</td>
</tr>
<tr>
<td>LogLevel</td>
<td>Level of log</td>
</tr>
<tr>
<td>LogFile</td>
<td>Filename of log</td>
</tr>
<tr>
<td>DataBaseConnUrl</td>
<td>mongodb connection address</td>
</tr>
<tr>
<td>DataBaseName</td>
<td>mongodb database name</td>
</tr>
</table>

##### chart_service Configurations：
<a name="chart_service">

	{
		"WriteLog": true,
		"LogLevel": "debug",
		"LogFile": "scan-api.log",
		"DataBaseConnUrl":"127.0.0.1:27017",
		"DataBaseName":"seele",
		"ShardCount":20
	}
</a>
<table> <tbody>
<tr>
<th>Service</th>
<th>Parameter</th>
<th>Explanation</th>
</tr>
<tr>
<th rowspan="8">chart_service</th>
<td>WriteLog</td>
<td>Switch for log read/write</td>
</tr>
<tr>
<tr>
<td>LogLevel</td>
<td>Level of log</td>
</tr>
<tr>
<td>LogFile</td>
<td>Filename of log</td>
</tr>
<tr>
<td>DataBaseConnUrl</td>
<td>mongodb connection address</td>
</tr>
<tr>
<td>DataBaseName</td>
<td>mongodb database name</td>
</tr>
<tr>
<td>ShardCount</td>
<td>Number of shards</td>
</tr>
</table>
##### node_service Configurations
<a name="node_service">

	{
		"RpcNodes" : ["0.0.0.0:55026"],
		"WriteLog": true,
		"LogLevel": "debug",
		"LogFile": "node_service.log",
		"DataBaseConnUrl":"127.0.0.1:27017",
		"DataBaseName": "seele",
		"Interval": 60,
		"ExpireTime": 60
	}
</a>
<table> <tbody>
<tr>
<th>Service</th>
<th>Parameter</th>
<th>Explanation</th>
</tr>
<tr>
<th rowspan="9">node_service</th>
<td>RpcNodes</td>
<td>seele node's RPC address list</td>
</tr>
<tr>
<tr>
<td>WriteLog</td>
<td>Switch for log read/write</td>
</tr>
<tr>
<td>LogLevel</td>
<td>Level of log</td>
</tr>
<tr>
<td>LogFile</td>
<td>Filename of log</td>
</tr>
<tr>
<td>DataBaseConnUrl</td>
<td>mongodb connection address</td>
</tr>
<tr>
<td>DataBaseName</td>
<td>mongodb database name</td>
</tr>
<tr>
<td>Interval</td>
<td>rpc connection time interval</td>
</tr>
<tr>
<td>ExpireTime</td>
<td>Expiration time of seele node</td>
</tr>
</table>

#### 3）Start scan-api：
##### Start order
  - mongodb：
    - In the command window, run: ./mongod -f ./mongod.conf

  - go-seele:
    - Start the go-seele node, refer to [Getting-Started-With-Seele](Getting-Started-With-Seele.html)

  - seele-syncer：
    - In the command window, run： ./seele_syncer -c ./server.json

  - scan_server：
    - In the command window, run： ./scan_server -c ./server.json

  - chart_service：
    - In the command window, run： ./chart_service： -c ./server.json

  - node_service：
    - In the command window, run： ./node_service： -c ./server.json
### 2. Deploy scan
#### 1) Download scan Source Code
```bash
git clone https://github.com/seeleteam/scan
```
#### 2） Modify scan Configuration
In the development environment, modify the config file `config/dev.env.js`
```bash
NODE_ENV: '"development"',  // dev mode
NEW_WORK_ID: 2,  // net work type, ex: 1 main 2 test
SCAN_SHARD: 20, // seele node shard total num
SCAN_API_URL: '"http://localhost:3003"', // scan-api url
SCAN_API_PATH: '"/api/v1"' // scan-api path
```
In the production environment, modify the config file `config/prod.env.js`
```bash
NODE_ENV: '"production"', // prod mode
NEW_WORK_ID: 2, // net work type, ex: 1 main 2 test
SCAN_SHARD: 20, // seele node shard total num
SCAN_API_URL: '"http://localhost:3003"', // scan-api url
SCAN_API_PATH: '"/api/v1"' // scan-api path
```
#### 3）Install and Compile the Code
```bash
cd scan
npm install
npm run build
```
#### 4) Start scan
##### Development Environment
```bash   
cd ./scan
npm run dev
```
##### Production Environment
```bash
Modify nginx config file `conf.d/scan.conf`
   server {
        listen      3002;
        server_name  _;
        root         /usr/local/nginx/scan;
        location / {
            index  index.html index.htm;
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }
cp -r ./scan/dist  /usr/local/nginx/scan
nginx -s reload
```
#### 5) Visit `scan http://localhost:3002` on your browser

## III. Seele Dashboard Deployment Steps

### 1. Install Required Tools
#### 1）	Install node
```bash
yum install node
```
#### 2）	Install nginx
```bash
yum install nginx
```
#### 3）	Install influxdb
```bash
https://dl.influxdata.com/influxdb/releases/influxdb-1.5.1.x86_64.rpm 
yum localinstall influxdb-1.5.1.x86_64.rpm
```
### 2. Start the Seele Node

### 3. Deploy dashboard-api
#### 1)	Download dashboard-api Source Code
```bash
git clone https://github.com/seeleteam/dashboard-api
```
#### 2)	Compile dashboard-api
```bash
cd dashboard-api
make
```
#### 3)	Modify dashboard-api Configurations
Modify the config file: `config/app.json`
```bash
{
    "Name": "dashboard-api", // dashboard api name
    "Version": "1.0",
    "ListenAddr": "0.0.0.0:61001", // dashboard api listen address
    "LogLevel":"debug",
    "DisableConsoleColor":true,
    "PrintLog":true,
    "WriteLog":true,
    "LimitConnection":0,
    "RunMode":"debug",
    "RootRouterPrefix":"/api",
    "ServerConfig":{
      "ReadTimeout":60,
      "WriteTimeout":60,
      "IdleTimeout":120,
      "MaxHeaderBytes":1048576
    },
    "DB":{                             // influxdb config
      "Name":"influxdb",               // influxdb link name
      "Addr":"http://localhost:8086",  // influxdb link address
      "UserName":"test",               // influxdb link username
      "Password":"test123",            // influxdb link password
      "DBInitialSize":5,
      "DBMaxActive":20,
      "DBIdleTimetout":30
    }
  }
```
#### 4)	Start dashboard-api
```bash
./dashboard-api start -c config/app.json
```
### 4. Deploy dashboard
#### 1)	Download dashboard Source Code
```bash
git clone https://github.com/seeleteam/dashboard
```
#### 2） Modify the Confirguations
Modify the Config file: `src/utils/config.js`
```bash
const API_URL = 'http://localhost:61001' // dashboard-api server url
```
Modifify the file：`package.json`
``` bash
"scripts": 
{
  "analyze": "cross-env PORT=8000 ANALYZE=1 BABELRC=1 umi build", // dashboard-port: PORT=8000
  "start": "cross-env PORT=8000 BABELRC=1 COMPILE_ON_DEMAND=none BROWSER=none HOST=0.0.0.0 umi dev", // dashboard-port: PORT=8000
  "lint": "eslint --fix --ext .js src",
  "build": "cross-env PORT=8000 BABELRC=1 umi build", // dashboard-port: PORT=8000
  "test": "umi test"
}
```
#### 3）Install and Compile the Code
``` bash
cd dashboard
npm install
npm run build
```
#### 4) Start dashboard Service
##### Development Environment
```bash
cd ./dashboard
npm run start
```   
##### Production Environment
```bash
nginx config file: conf.d/dashboard.conf
   server {
        listen      8000;
        server_name  _;
        root         /usr/local/nginx/dashboard;
        location / {
            index  index.html index.htm;
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }
cp -r ./dashboard/dist  /usr/local/nginx/dashboard
nginx -s reload
```

#### 5) Visit `dashboard http://localhost:8000` in your browser
