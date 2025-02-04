srv6 traceroute tool
=============

Usage
-----

::

    usage: srv6_traceroute.py [-h] (-d DESTINATION | -f DESTINATION_FILE)
                              [-c COUNT] [-s PACKETSIZE] [-t TIMEOUT]
                              [-v VERBOSITY]

    SRv6 traceroute script

    optional arguments:
      -h, --help            show this help message and exit
      -d DESTINATION, --destination DESTINATION
                            Destination host IPv6
      -f DESTINATION_FILE, --destination_file DESTINATION_FILE
                            File with destination hosts IPv6
      -c COUNT, --count COUNT
                            Count of random IPv6 SR hops
      -l SIDS_FILE, --list_of_sids SIDS_FILE
                            Json file with a custom sid list 
      -s PACKETSIZE, --packetsize PACKETSIZE
                            ICMP echo packet data size
      -t TIMEOUT, --timeout TIMEOUT
                            Scapy packet timeout
      -v VERBOSITY, --verbosity VERBOSITY
                            Scapy verbosity

Example of DESTINATION\_FILE is in the file ``hosts.yml.example``.

Sample output
-------------

Single traceroute
~~~~~~~~~~~~~~~~~

::

    -> srv6_traceroute.py -d dead:beef:ca1f
    ======= Starting ICMP (packet size: 8) traceroute to dead:beef:ca1f =======
    ======= Starting SRv6 (packet size: 8) traceroute to dead:beef:ca1f =======
    +-----+-----------------------------+-------------------------+-------------------------+--------------------+
    | TTL |             ASN             |         ICMP dst        |          SR dst         |      Latency       |
    +-----+-----------------------------+-------------------------+-------------------------+--------------------+
    |  1  |              -              |            -            |            -            |         -          |
    |  2  |              -              |            -            |            -            |         -          |
    |  3  | AS-CHOOPA - Choopa, LLC, US | 2001:19f0:5000::a48:131 |            -            | 9.755134582519531  |
    |  4  |         AMS-IX1, NL         | 2001:7f8:1::a502:4940:1 | 2001:7f8:1::a502:4940:1 | 44.83842849731445  |
    |  5  |        HETZNER-AS, DE       |    2a01:4f8:0:3::11d    |    2a01:4f8:0:3::11d    | 24.158716201782227 |
    |  6  |        HETZNER-AS, DE       |     2a01:4f8:0:3::f9    |     2a01:4f8:0:3::f9    | 27.796506881713867 |
    |  7  |        HETZNER-AS, DE       |  2a01:4f8:0:e0c0::a002  |  2a01:4f8:0:e0c0::a002  | 33.812522888183594 |
    |  8  |              -              |            -            |            -            |         -          |
    |  9  |        HETZNER-AS, DE       |  2a01:4f8:0:e0c0::1c16  |  2a01:4f8:0:e0c0::1c16  | 20.31564712524414  |
    |  10 |              -              |            -            |            -            |         -          |
    |  11 |        HETZNER-AS, DE       |      dead:beef:ca1f     |      dead:beef:ca1f     | 17.747879028320312 |
    +-----+-----------------------------+-------------------------+-------------------------+--------------------+

Multi destination traceroute
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    -> srv6_traceroute.py -f hosts.yml
    Performing traceroute on server host1 (dead:beef:ca1f)
    ======= Starting ICMP (packet size: 8) traceroute to dead:beef:ca1f =======
    ======= Starting SRv6 (packet size: 8) traceroute to dead:beef:ca1f =======
    Results of traceroute to server host1 (dead:beef:ca1f)
    +-----+----------------+-------------------------+-------------------------+--------------------+
    | TTL |      ASN       |         ICMP dst        |          SR dst         |      Latency       |
    +-----+----------------+-------------------------+-------------------------+--------------------+
    |  1  |       -        |            -            |            -            |         -          |
    |  2  |       -        |            -            |            -            |         -          |
    |  3  |       -        |            -            |            -            |         -          |
    |  4  |  AMS-IX1, NL   | 2001:7f8:1::a502:4940:1 | 2001:7f8:1::a502:4940:1 | 7.732629776000977  |
    |  5  | HETZNER-AS, DE |    2a01:4f8:0:3::11d    |    2a01:4f8:0:3::11d    | 14.463424682617188 |
    |  6  | HETZNER-AS, DE |     2a01:4f8:0:3::f9    |     2a01:4f8:0:3::f9    | 18.020153045654297 |
    |  7  | HETZNER-AS, DE |  2a01:4f8:0:e0c0::a002  |  2a01:4f8:0:e0c0::a002  | 17.49587059020996  |
    |  8  |       -        |            -            |            -            |         -          |
    |  9  | HETZNER-AS, DE |  2a01:4f8:0:e0c0::1c16  |  2a01:4f8:0:e0c0::1c16  | 17.79937744140625  |
    |  10 |       -        |            -            |            -            |         -          |
    |  11 | HETZNER-AS, DE |     dead:beef:ca1f      |      dead:beef:ca1f     | 16.185998916625977 |
    +-----+----------------+-------------------------+-------------------------+--------------------+
    Performing traceroute on server host2 (1d1e:f001)
    ======= Starting ICMP (packet size: 8) traceroute to 1d1e:f001 =======
    ======= Starting SRv6 (packet size: 8) traceroute to 1d1e:f001 =======
    Results of traceroute to server host2 (1d1e:f001)
    +-----+-----------------------------+-------------------------+-------------------------+--------------------+
    | TTL |             ASN             |         ICMP dst        |          SR dst         |      Latency       |
    +-----+-----------------------------+-------------------------+-------------------------+--------------------+
    |  1  |              -              |            -            |            -            |         -          |
    |  2  |              -              |            -            |            -            |         -          |
    |  3  | AS-CHOOPA - Choopa, LLC, US | 2001:19f0:5000::a48:131 | 2001:19f0:5000::a48:131 | 22.018909454345703 |
    |  4  |         AMS-IX1, NL         | 2001:7f8:1::a502:4940:1 | 2001:7f8:1::a502:4940:1 | 7.369518280029297  |
    |  5  |        HETZNER-AS, DE       |    2a01:4f8:0:3::11d    |    2a01:4f8:0:3::11d    | 12.90130615234375  |
    |  6  |        HETZNER-AS, DE       |     2a01:4f8:0:3::b2    |     2a01:4f8:0:3::b2    | 18.60523223876953  |
    |  7  |        HETZNER-AS, DE       |     2a01:4f8:0:3::ee    |     2a01:4f8:0:3::ee    | 19.85001564025879  |
    |  8  |        HETZNER-AS, DE       |        1d1e:f001        |        1d1e:f001        | 19.013166427612305 |
    +-----+-----------------------------+-------------------------+-------------------------+--------------------+


