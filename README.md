# pod-daq-analyzer

This repo contains code to support the logging of data acquisition packets
and their analysis.

## Subprojects

The major subprojects (subdirectories are):

  * pi3-buildroot - Buildroot configuration for Raspberry Pi 3,
    which serves as the host data logger running "tcpdump".
    The "tcpdump" utility may be replaced later by a real-time logger
    which is tailored to specific needs of the overall project.
  * capextract - Extraction of data from captured packets and
    conversion to CSV.  This is dependent on the packet definitions for
    each of the reporting controls or sensors.
    The CSV conversion may be done on the RaspPi3, or the data may
    be downloaded after flight to a laptop or desktop and converted
    there.
  * daqparse - Interpretation of CSV data, possibly in Python and
    Bokeh.  This is expected to run on laptop or desktop.

A logger other than "tcpdump" may eventually be created.  In that
case, there may be another project:

  * logger - listens for specific network traffic, and stores it
    into log files, for later processing.  Alternatively, selected
    packets may be forwarded to a capextract thread/process for
    immediate consumption.

## Possible use cases

The current architecture assumes real-time capture and logging of data
packets by "tcpdump"; subsequent extraction of data and conversion to
CSV depend on the logging media (microSD card) being removed from
the pod in non-real-time.

There are possible variations to this.  All start with:

  * Real-time capture and logging of packets in a 'capture thread'.

The capture thread may filter certain data channels for:

  * immediate conversion to CSV.
  * collection of channel min/max values for periodic transmission
    to a ground station.

