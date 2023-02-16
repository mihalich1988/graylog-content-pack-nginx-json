# graylog-content-pack-nginx-json


### Configuring nginx

You need to run at least nginx version 1.11.8, with `escape=json` support.

**Add this to your nginx configuration file and restart the service:**

    log_format graylog_json escape=json '{'
                                                '"connection_id": $connection,'
                                                '"connection_requests": $connection_requests,'
                                                '"timestamp": $msec,'
                                                '"remote_addr": "$remote_addr",'
                                                '"millis": $request_time,'
                                                '"response_status": $status,'
                                                '"response_bytes": $body_bytes_sent,'
                                                '"request": "$request",'
                                                '"request_id": "$request_id",'
                                                '"request_verb": "$request_method",'
                                                '"request_bytes": $request_length,'
                                                '"request_scheme": "$scheme",'
                                                '"request_path": "$request_uri",'
                                                '"http_host": "$host",'
                                                '"http_x_forwarded_for": "$http_x_forwarded_for",'
                                                '"http_x_real_ip": "$http_x_real_ip",'
                                                '"http_x_client_ip": "$http_x_client_ip",'
                                                '"http_referer": "$http_referer",'
                                                '"http_user_agent": "$http_user_agent",'
                                                '"http_version": "$server_protocol",'
                                                '"server_addr": "$server_addr",'
                                                '"server_port": "$server_port",'
                                                '"server_name": "$server_name",'
                                                '"upstream_cache_status": "$upstream_cache_status",'
                                                '"upstream_status": "$upstream_status",'
                                                '"upstream_millis": "$upstream_response_time",'
                                                '"upstream_addr": "$upstream_addr",'
                                                '"upstream_connect_time": "$upstream_connect_time",'
                                                '"upstream_response_length": "$upstream_response_length",'
                                                '"https": "$https",'
                                                '"ssl_cipher": "$ssl_cipher",'
                                                '"ssl_protocol": "$ssl_protocol",'
                                                '"ssl_server_name": "$ssl_server_name",'
                                                '"ssl_session_id": "$ssl_session_id",'
                                                '"ssl_session_reused": "$ssl_session_reused",'
                                                '"proxy_protocol_addr": "$proxy_protocol_addr",'
                                                '"proxy_protocol_port": "$proxy_protocol_port",'
                                                '"proxy_protocol_server_addr": "$proxy_protocol_server_addr",'
                                                '"proxy_protocol_server_port": "$proxy_protocol_server_port"'
                                         '}';

    # replace the %graylog% with the IP or hostname of your Graylog server
    access_log syslog:server=%graylog%:12401,tag=nginx_nginx graylog_json;
    error_log syslog:server=%graylog%:12402;
    
You can use different syslog `tag` for your sites. For example:

    # access_log syslog:server=%graylog%:12401,tag=site1_nginx graylog_json;
    # access_log syslog:server=%graylog%:12401,tag=site2_nginx graylog_json;
    # access_log syslog:server=%graylog%:12401,tag=site3_nginx graylog_json;
    
This tag will be in `nginx_config` parameter in Graylog.
