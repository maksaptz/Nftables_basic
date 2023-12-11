```flush ruleset

table inet filter {
        chain input {
                type filter hook input priority 0;
                policy drop;
                ct state {established, related} accept
                ip protocol icmp counter accept
                iif lo accept
                ct state invalid drop
                tcp dport ssh counter accept
        }

        chain forward {
                type filter hook forward priority filter;
                policy drop;
        }

        chain output {
                type filter hook output priority filter;
                policy accept;
        }
}```
