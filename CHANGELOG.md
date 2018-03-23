# Change log

This file contains al notable changes to the bertvv.tomcat Ansible role. This file adheres to the guidelines of [http://keepachangelog.com/](http://keepachangelog.com/). Versioning follows [Semantic Versioning](http://semver.org/).

## 1.1.2 - 2016-06-16

## Changed

- Use the generic package module
- Don't initialize Jasper Reports, this doesn't work on Tomcat 8 (Fedora)

## 1.1.1 - 2016-06-14

### Changed

- (GH-2) Set the owner/group of .war files
- Changed the tomcat user into a variable instead of a hard coded value.

## 1.1.0 - 2016-04-22

### Added

- Support for Fedora 23

## 1.0.0 - 2016-04-20

First release!

### Added

- Install Tomcat from EPEL, allow installation of libraries in `$CATALINA_HOME/lib/` and deployment of webapp archive files (.war)

