# Legrand fork
## How to maintain this fork
On master branch, cherry pick modification done on upstream master branch.
To port Legrand modification on a release, start a branch on the release commit then cherry pick modification done on previous branch.

## List of modification

- Add the link to the execution profile kit if defined
- nx_packet_pool_min_available
- Add #define TLS_PSK_WITH_AES_128_GCM_SHA256                    0x00A8
- Group server hello, key exchange and hello done messages
- _nx_secure_x509_parse_public_key NOT in static (Used for Binary_package validation)
- DTLS manage fragmented packet
- Check if fragment can fit in a single packet
- Fix warning on GCC 12.2 (stdint.h not include by default)
- MQTT : Fix issue when we receive a too big TOPIC or Payload. (Release the packet if we don't have enough space to handle it)
- PPP workaround for https://github.com/eclipse-threadx/netxduo/issues/340

## Previous modification (v6.2.0_legrand) which are not reported
- _nx_tcpserver_tls_setup() init ECC (for elliptic curve algo : ECDSA.... )
In app, call nx_tcpserver_tls_ecc_setup() after nx_tcpserver_tls_setup() to setup the elliptic curve support
- Check if nx_interface_link_driver_entry != NULL before call it: fix in v6.2.1 of upstream repo
- On DHCP request, ask for NTP server: Use nx_dhcp_user_option_request() instead to define the needed options in DHCP request