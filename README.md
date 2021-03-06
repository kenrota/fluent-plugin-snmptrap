# Fluent::Plugin::SnmpTrap

fluent-plugin-snmptrap is an input plug-in for [Fluentd](http://fluentd.org)

## Status
[![Gem Version](https://badge.fury.io/rb/fluent-plugin-snmptrap.png)](http://badge.fury.io/rb/fluent-plugin-snmptrap)
[![Build Status](https://travis-ci.org/Bigel0w/fluent-plugin-snmptrap.png?branch=master)](https://travis-ci.org/Bigel0w/fluent-plugin-snmptrap)
[![Coverage Status](https://coveralls.io/repos/Bigel0w/fluent-plugin-snmptrap/badge.png?branch=master)](https://coveralls.io/r/Bigel0w/fluent-plugin-snmptrap?branch=master)

## Installation

These instructions assume you already have fluentd installed. 
If you don't, please run through [quick start for fluentd] (https://github.com/fluent/fluentd#quick-start)

Now after you have fluentd installed you can follow either of the steps below:

Add this line to your application's Gemfile:

    gem 'fluent-plugin-snmptrap'

Or install it yourself as:

    $ gem install fluent-plugin-snmptrap

## Usage
Add the following into your fluentd config.

    <source>
      type snmptrap       # required, chossing the input plugin.
      host 127.0.0.1      # optional, interface to listen on, default 0 for all.
      port 162            # optional, port to listen for traps, default is 1062
                          # ports under 1024 range will require sudo to start fluentd
      tag alert.snmptrap  # optional, tag to assign to events, default is alert.snmptrap 
    </source>
    
    <match alert.snmptrap>
      type stdout
    </match>
    
Now startup fluentd

    $ sudo fluentd -c fluent.conf &
    
Send a test trap using net-snmp tools
    
    & sudo snmptrap -v 1 -c public localhost:1062 1.3.6.1.4.1.10300.1.1.1.12 localhost 3 0 ''  
  
## To Do
Things left to do, not in any particular order.
* wrap snmp-trap listener and have it restart on failure.
* add support for loading MIBs
* explode the var binds
* snmp-trap output plug-in that exposes common fields and lets them be overwritten before forwarding.                