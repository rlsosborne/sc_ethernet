XCORE.com ETHERNET SOFTWARE COMPONENT
.................................

:Latest release: 2.3.2rc0
:Maintainer: DavidNorman
:Description: A complete Ethernet MII and MAC interface for 100MBps Ethernet


Key Features
============

   * RX and TX on separate logical cores
   * Packet filtering by extension function
   * Memory based locking protocol
   * FIFO based memory allocation for lower RAM overhead
   * High priority (VLAN priority tag) queues
   * 802.1Qat traffic shaping
   
Low thread count MII driver
===========================

An alternative, low core count MII driver is available.

   * MII pins in 1 logical core
   * Rx buffer support handled by interrupt in a designated second
     task on a different core
   * Optional service task for providing an API similar to the
     5-thread implementation

Firmware Overview
=================

RX and TX are defined as functions which each run on their own logical
core. Core usage is 5 logical cores for a single port (reducible to 4
for lower bandwith transmit applicatio).  Ports must be MII and
attached to the same xcore.

Known Issues
============

   * The rx_packet-rx_packet timing constraint may fail because of the user defined packet filters. The user
     is required to fill in the timing details inside any user specified filter in order to help the XTA
     analyze the receive filter timing correctly.
   * Packets exceeding the Ethernet maximum length can cause system crash
   * Does not reject Ethernet/Ethernet-II/Ethernet-DIX encoded frames where the frame length does not match the length field 

Support
=======

Issues may be submitted via the Issues tab in this github repo. Response to any issues submitted as at the discretion of the maintainer for this line.

Required software (dependencies)
================================

  * sc_util (git@github.com:xcore/sc_util)
  * sc_slicekit_support (git@github.com:xcore/sc_slicekit_support)
  * sc_otp (git@github.com:xcore/sc_otp)

