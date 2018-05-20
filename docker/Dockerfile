FROM haproxy:1.8
ADD haproxy.cfg /usr/local/etc/haproxy/
ADD 503.http /usr/local/etc/haproxy/errors/
CMD haproxy -f /usr/local/etc/haproxy/haproxy.cfg
