shodan download query Allworx  --limit -1


shodan download query  Mikrotik
shodan init PSKINdQe1GyxGgecYz2191H2JoS9qvgD
============================================
shodan download --limit -1 product:apache country:AU
shodan download --limit -1 product:nginx country:AU
shodan download --limit -1 product:Microsoft-HTTPAPI country:AU
shodan download --limit -1 product:AkamaiGHost country:AU
shodan download --limit -1 product:httpd country:AU
shodan download --limit -1 product:Microsoft-IIS country:AU
==============================================


shodan stats --facets ip_str,port product:apache country:US

shodan parse --fields ip_str,port --separator , domain.json.gz

shodan download --limit -1 product:apache country:US


shodan download search --fields ip_str,port,query BW HTTP Server

shodan download query  broadworks
shodan parse --fields ip_str,port --separator , broadworks.json.gz  تحليل ملف تم انشاءه


shodan parse --fields domains,port --separator , domain.json.gz

shodan download query hostname:"cfg."

shodan search ip:194.177.50.24

shodan convert CVE-2019-0708.json.gz  csv   تحويل الامتداد
vuln: والثغرة

shodan search  product:apache country:US
shodan stats product:apache

Properties

asn
    [String] The autonomous system number (ex. "AS4837").
data
    [String] Contains the banner information for the service.
ip
    [Integer] The IP address of the host as an integer.
ip_str
    [String] The IP address of the host as a string.
ipv6
    [String] The IPv6 address of the host as a string. If this is present then the "ip" and "ip_str" fields wont be.
port
    [Integer] The port number that the service is operating on.
timestamp
    [String] The timestamp for when the banner was fetched from the device in the UTC timezone. Example: "2014-01-15T05:49:56.283713"
hostnames
    [String[]] An array of strings containing all of the hostnames that have been assigned to the IP address for this device.
domains
    [String[]] An array of strings containing the top-level domains for the hostnames of the device. This is a utility property in case you want to filter by TLD instead of subdomain. It is smart enough to handle global TLDs with several dots in the domain (ex. "co.uk")
location
    [Object] An object containing all of the location information for the device.
location.area_code
    [Integer]The area code for the device's location. Only available for the US.
location.city
    [String] The name of the city where the device is located.
location.country_code
    [String] The 2-letter country code for the device location.
location.country_code3
    [String] The 3-letter country code for the device location.
location.country_name
    [String] The name of the country where the device is located.
location.dma_code
    [Integer] The designated market area code for the area where the device is located. Only available for the US.
location.latitude
    [Double] The latitude for the geolocation of the device.
location.longitude
    [Double] The longitude for the geolocation of the device.
location.postal_code
    [String] The postal code for the device's location.
location.region_code
    [String] The name of the region where the device is located.
opts
    [Object] Contains experimental and supplemental data for the service. This can include the SSL certificate, robots.txt and other raw information that hasn't yet been formalized into the Banner Specification.
org
    [String] The name of the organization that is assigned the IP space for this device.
isp
    [String] The ISP that is providing the organization with the IP space for this device. Consider this the "parent" of the organization in terms of IP ownership.
os
    [String] The operating system that powers the device.
transport
    [String] Either "udp" or "tcp" to indicate which IP transport protocol was used to fetch the information


Optional Properties

uptime
    [Integer] The number of minutes that the device has been online.
link
    [String] The network link type. Possible values are: "Ethernet or modem", "generic tunnel or VPN", "DSL", "IPIP or SIT", "SLIP", "IPSec or GRE", "VLAN", "jumbo Ethernet", "Google", "GIF", "PPTP", "loopback", "AX.25 radio modem".
title
    [String] The title of the website as extracted from the HTML source.
html
    [String] The raw HTML source for the website.
product
    [String] The name of the product that generated the banner.
version
    [String] The version of the product that generated the banner.
devicetype
    [String] The type of device (webcam, router, etc.).
info
    [String] Miscellaneous information that was extracted about the product.
cpe
    [String] The relevant Common Platform Enumeration for the product or known vulnerabilities if available. For more information on CPE and the official dictionary of values visit the CPE Dictionary. 


SSL Properties

If the service uses SSL, such as HTTPS, then the banner will also contain a property called "ssl":

ssl.cert
    [Object] The parsed certificate properties that includes information such as when it was issued, the SSL extensions, the issuer, subject etc.
ssl.cipher
    [Object] Preferred cipher for the SSL connection
ssl.chain
    [Array] An array of certificates, where each string is a PEM-encoded SSL certificate. This includes the user SSL certificate up to its root certificate.
ssl.dhparams
    [Object] The Diffie-Hellman parameters if available: "prime", "public_key", "bits", "generator" and an optional "fingerprint" if we know which program generated these parameters.
ssl.versions
    [Array] A list of SSL versions that are supported by the server. If a version isnt supported the value is prefixed with a "-". Example: ["TLSv1", "-SSLv2"] means that the server supports TLSv1 but doesnt support SSLv2. 

shodan: The official Python library and CLI for Shodan
======================================================

.. image:: https://img.shields.io/pypi/v/shodan.svg
    :target: https://pypi.org/project/shodan/

.. image:: https://img.shields.io/github/contributors/achillean/shodan-python.svg
    :target: https://github.com/achillean/shodan-python/graphs/contributors

Shodan is a search engine for Internet-connected devices. Google lets you search for websites,
Shodan lets you search for devices. This library provides developers easy access to all of the
data stored in Shodan in order to automate tasks and integrate into existing tools.

Features
--------

- Search Shodan
- `Fast/ bulk IP lookups <https://help.shodan.io/developer-fundamentals/looking-up-ip-info>`_
- Streaming API support for real-time consumption of Shodan firehose
- `Network alerts (aka private firehose) <https://help.shodan.io/guides/how-to-monitor-network>`_
- `Manage Email Notifications <https://asciinema.org/a/7WvyDtNxn0YeNU70ozsxvXDmL>`_
- Exploit search API fully implemented
- Bulk data downloads
- `Command-line interface <https://cli.shodan.io>`_

.. image:: https://cli.shodan.io/img/shodan-cli-preview.png
    :target: https://asciinema.org/~Shodan
    :width: 400px
    :align: center


Quick Start
-----------

.. code-block:: python

    from shodan import Shodan

    api = Shodan('MY API KEY')

    # Lookup an IP
    ipinfo = api.host('8.8.8.8')
    print(ipinfo)

    # Search for websites that have been "hacked"
    for banner in api.search_cursor('http.title:"hacked by"'):
        print(banner)

    # Get the total number of industrial control systems services on the Internet
    ics_services = api.count('tag:ics')
    print('Industrial Control Systems: {}'.format(ics_services['total']))

Grab your API key from https://account.shodan.io

Installation
------------

To install the Shodan library, simply:

.. code-block:: bash

    $ pip install shodan

Or if you don't have pip installed (which you should seriously install):

.. code-block:: bash

    $ easy_install shodan


Documentation
-------------

Documentation is available at https://shodan.readthedocs.org/ and https://help.shodan.io
