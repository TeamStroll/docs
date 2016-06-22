# Setting Up You Local Dev Environment

## Killing the Process

`ps -ef`: To find where the java process is running, grab the middle two four digit numbers

`kill [numbers]`: Kills the process

## To Test if the Connection is Working

`curl "http://localhost:9090/sh/payers" -X "GET" "MediaType: application/vnd.sh-v1.0+json" -H "apikey: thisisdummyapikeysignature" -H "content-type:application/json"`

## GC Memory Limit?

Open your run configurations, and add `-Xmx2048m` under vm
