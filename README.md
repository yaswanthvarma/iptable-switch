# iptable-switch




**on App1**   : nc -l -p 2020
**on App2**   : nc -l -p 2021

**On router** : 
nc -zv -w2 192.168.1.12 2020
nc -zv -w2 192.168.1.13 2021


#####################################################
# Delete forwarding rule to App1:2020
iptables -t nat -D PREROUTING -p tcp --dport 2020 -j DNAT --to-destination 192.168.1.12:2020

# Forwarding rule to App2 on 2021
iptables -t nat -A PREROUTING -p tcp --dport 2020 -j DNAT --to-destination 192.168.1.13:2021
####################################################
