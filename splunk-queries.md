# Splunk Queries Used

## Finding 1: Hakai Botnet Command Injection
```spl
index=botsv3 earliest=0 source="/var/log/httpd/access_log" "Hakai"
| table _time, _raw
```

## Finding 2: klagerfield Bash History Review
```spl
index=botsv3 earliest=0 source="/home/klagerfield/.bash_history" host="hoth"
| sort _time
| table _time, _raw
```

## Finding 3: AWS GuardDuty Port Probe
```spl
index=botsv3 earliest=0 "GuardDuty Finding"
| spath
| table _time, detail.type, detail.title, detail.severity, detail.service.action.portProbeAction.remoteIpDetails.ipAddressV4, detail.service.action.portProbeAction.remoteIpDetails.country.countryName
```

## Finding 4: DNS Traffic Sweep
```spl
index=botsv3 earliest=0 sourcetype="stream:dns"
| stats count by query
| sort -count
```
