# capextract - extract data from captured packets

This subproject is intended to extract the payload portion of captured IPv4
(usually UDP) packets, and convert them into CSV files which can later be
viewed by analysis programs.

## Requirements

The packets are currently captured (logged) by Unix/Linux "tcpdump", and
are thus stored with corresponding "libpcap" meta-data.  The extractor(s)
will need to parse beyond the meta-data, IPv4, and other protocol layers to
get at the data acquired through DAQ processes.

The extractor will need to recognize the type of data, according to an
early field in the payload, and make the data available to the converter.
The extractor acts as the interface between the host data logger
(currrently "tcpdump") and application-specific data.  It should be
possible to change out the data logger without impacting the
downstream services, e.g., the converter.

The converter interprets the data according to DAQ configuration files,
resulting in CSV files.  The converter may run on the same system as the
data logger or on machine external to the pod, e.g., a laptop or desktop
machine.

## References

  * pcap-savefile -
    http://www.tcpdump.org/manpages/pcap-savefile.5.html
