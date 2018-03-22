Robust Laboratory Digital Signal Distribution
================================================================================
Experimental work often involves digital signals for various devices in order to
control the function, timing, and state of the output for these various devices.
Additionally, laboratory environments typically contain various electromagnetic
interference (EMI) sources, including the digital signals themselves.

AFRL's digital signal distribution hardware mitigates some of the challenges of
EMI that may originate either from digital signals or corrupt digital signal
transmission.  The digital signal distribution hardware supports the low-noise
transport of asynchronous timing signals through a laboratory-grade hostile EMI
environment by converting single-ended TTL signals to LVDS for transmission over
standard Cat-5e/Cat-6 twisted pair (Ethernet) cables to 4-channel receiver boxes
which return the signals to 3.3 or 5~V (LV)TTL signals suitable for interfacing
with rack or bench instrumentation.  The receiver boxes are locally powered and
decoupled from the LVDS ground potential to minimize the creation of ground
loops compared to direct wiring of TTL signals from the source instrument.
Inputs to the transmitter board are connected through a 68-pin VHDCI connector.

License
--------------------------------------------------------------------------------
The hardware schematics are made available under the CERN Open Hardware Licence
version 1.2 or later.


Components of Project
--------------------------------------------------------------------------------

  - _Digital Signal Transmission ("transmitter" sub-directory):_

    Digital board design that can be used to convert digital LVTTL signals into
    LVDS signals for transmission accross a laboratory or other EMI-noisy
    environments.  This board was originally developed to convert the signals
    from a Marvin-Test GX3500 FPGA card executing firmware from the AFRL/Timing
    Generator project.

    Each board includes:
      - A single VHDCI connector.  This connector can be used used to connect to
        the source of the set of signals which will be converted to LVDS.
        Nominally, this connector is meant to attach to one of the ports of the
        GX3500 FPGA card from Marvin Test Solutions, Inc.

      - A single BNC connection that can be used to provide some type of trigger
        signal as implemented by the hardware/firmware to which this board is
        connected via the VHDCI connector.  For the AFRL/Timing Generator
        firmware, this signal input is used to trigger digital waveform
        generation.

      - 8 RJ45 ports, each of which connects, via an CAT-5e or CAT-6 ethernet
        cable, to the Receiver board (see below).

  - _Digital Signal Receiver ("receiver sub-directory):_

    Digital board design to convert digital LVDS signals into either LVTTL or
    TTL signals.  The conversion occurs locally, after traversing the laboratory
    environment, using local ground and power definitions.

    Each board includes:
      - A single RJ45 port that is meant to connect to a LVDS driver as defined
        by or similar to the "transmitter" board described above.

      - Four BNC connections that can be used to export the LVTTL or TTL signals
        to local digital sinks.

      - A single switch that is used to select either LVTTL or TTL level
        signals to be exported over the four BNC connections.
