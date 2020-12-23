IPSEC PHASE 1 & 2 hQ
=============

en 
config t
crypto isakmp policy 1
hash md5
authen pre-share
group 2
encry aes
exit
crypto isakmp key cisco123 address 1.39.101.2
Access-list 100 permit ip 192.168.1.0 0.0.0.255 10.0.0.0 0.0.0.255
crypto ipsec transform-set myset esp-3des esp-md5-hmac
exit
crypto map hq-map 1 ipsec-isakmp
set peer 1.39.101.2 
Set transform-set myset
match address 100 
exit

int g0/0
crypto map hq-map




IPSEC PHASE 1 BR
=============

en 
config t
crypto isakmp policy 1
hash md5
authen pre-share
group 2
encry aes
exit
crypto isakmp key cisco123 address 199.1.1.2


ipsec phase 2 BR
---------------

Access-list 100 permit ip  10.0.0.0 0.0.0.255 192.168.1.0 0.0.0.255
crypto ipsec transform-set myset esp-3des esp-md5-hmac

crypto map br-map 1 ipsec-isakmp
set peer 199.1.1.2 
Set transform-set myset
match address 100 
exit

int g0/0
crypto map br-map
