# Quality Control Document

| Project | Mod Library |
| --- | --- |
| Part Number | A0015-300001 |
| Drafted By | Automated Tooling |
| Project Engineer | Eli Sells |
| Quality Assurance | Nicholas Armistead |

## Table of Contents

- [1. PROJECT OVERVIEW](#1-project-overview)
- [2. SUPPORTING DOCUMENTATION](#2-supporting-documentation)
- [3. REQUIREMENTS](#3-requirements)
- [4. DEVELOPMENT READINESS](#4-development-readiness)
- [5. COMPONENTS](#5-components)
- [6. TEST PROCEDURES](#6-test-procedures)
- [7. TEST READINESS](#7-test-readiness)
- [8. TEST RESULTS](#8-test-results)
- [9. FLIGHT QUALIFICATION](#9-flight-qualification)

# 1. PROJECT OVERVIEW

The mod library is a platform-independent utility library written in C that is used throughout SDR’s embedded C code. The library is composed of “components”, which are smaller libraries with dependencies on each other. Components may be further broken down into modules based on complexity.

Historically, the “mod” library was the sole common library at SDR used to house drivers and utilities side-by-side for use across projects. As of version 3.1.0, it has been made completely independent of external components except for any C standard library implementation.

The components in “mod” are optimized for embedded projects that run in low-power, low-memory, and low-speed environments. It is designed to be integrated into safety critical projects and follows SDR’s highest standard for software quality assurance. No dynamic memory allocation is used – all memory is scoped statically, on the stack, or provided by the integrating project.

## QUALITY ASSURANCE PRACTICES

The primary guiding standard for this project is the [SDR Software Quality Assurance Standard](https://docs.google.com/document/d/18T5YLIsYWkMpDS0G6ab43WqmqcFqEYc4my6OPZia8H4/edit?tab=t.0). This version of the library is intended to be used across all software projects, so it is certified as “Safety Critical”.

However, as a library, this project is unable to determine how it is used and is therefore unable to analyze its own hazards. Hazard analysis shall be performed by the integrating project. The architectural guidance for this project is therefore to let error handling be performed by whichever project is calling into it.

The mod library was designed so that no component sits on the system boundary. Validation is performed on “public” inputs to the library to prevent memory access faults and other memory related issues. Thus, the security surface of this software project is considered to be negligible.

# 2. SUPPORTING DOCUMENTATION

| Document | Description |
| --- | --- |
| [Doxygen Documentation (SDR Docs Server)](https://docs.sundevilrocketry.org/avionics/mod) | Living documentation from the repository in the _doc folder. Every push to “main” updates the documentation on the server. |

# 3. REQUIREMENTS

The article's requirements are defined in `_reqs/srd.md`.

# 4. DEVELOPMENT READINESS

The project meets the requirements to begin development:

- Requirements are defined
- Quality assurance practices have been defined and agreed upon

**Date:** 11/26/2026  
**Project Engineer:** Eli Sells  
**Quality Assurance:** Nicholas Armistead  

# 5. COMPONENTS

This project has no external dependencies.

# 6. TEST PROCEDURES

All test procedures for this article are defined in code under _test/mod.

All tests are performed at the unit level, with the exception of NAV, which has a software integration test for the component. The integrating project is responsible for any other integration tests.

# 7. TEST READINESS

The project has completed its initial development and is ready to enter the testing phase.

The project meets the requirements to begin testing:

- Development is complete and all requirements have been implemented
- Quality assurance practices have been followed, and an audit has been conducted on a random sample of constituent parts
- Test procedures have been defined and all requirements will be tested by the procedure

**Date:** 11/26/2026  
**Project Engineer:** Eli Sells  
**Quality Assurance:** Nicholas Armistead  

# 8. TEST RESULTS

The project has completed its test procedures and has produced the following results:

| Requirement tag | Requirement text | Results file | Test status |
| --- | --- | --- | --- |
| RQ.MOD.00002 | The library shall be organized into self-contained modules with header files organized next to source files. | mod/_test/mod/analysis_results.md | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00003 | The library shall be designed to be compiled with GNU GCC for the desired target architecture. | mod/_test/mod/analysis_results.md | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00004 | The library shall provide a ping response code based on the provided compiler macro from the project. | mod/_test/mod/commands/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00007 | The library shall provide a platform-independent method to log debug data. | mod/_test/mod/debug_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00008 | The debug logger shall use a circular buffer without dynamic memory allocation. | mod/_test/mod/debug_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00009 | The debug logger shall accept a callback to be used to write debug data asynchronously. | mod/_test/mod/debug_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00010 | The debug logger shall accept a callback to be used if the buffer overflows. | mod/_test/mod/debug_sdr/results.txt<br>mod/_test/mod/debug_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00011 | The debug logger shall provide a default implementation of the buffer overflow callback. | mod/_test/mod/debug_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00012 | The debug logger shall provide a function to be called after an asynchronous write completes. | mod/_test/mod/debug_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00013 | The library shall provide an error handler. | mod/_test/mod/error_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00014 | If the USE_ERROR_CALLBACK macro is defined, the error handler shall search a lookup table for a callback provided by the project given an error code. | mod/_test/mod/error_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00015 | The error handler shall provide an overridable default error callback if the lookup fails or USE_ERROR_CALLBACK is not defined. | mod/_test/mod/error_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00016 | The library shall provide a method to compute a Castagnoli 32-bit cyclic redundancy check. | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00040 | The library shall provide a method to clamp a float within a specified range. | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00017 | Hamilton Product (multiplication) | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00018 | Dot product | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00019 | Addition | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00020 | Scalar Multiplication | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00021 | Unit normalization | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00022 | Conjugation | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00047 | Creation from euler angles | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00048 | Determine whether quat is finite | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00049 | Body-to-world frame transition | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00050 | World-to-body frame transition | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00041 | Addition | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00042 | Cross Product | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00043 | Determine whether vector is finite | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00044 | Determine magnitude | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00045 | Normalization | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00046 | Scalar Multiplication | mod/_test/mod/math_sdr/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00051 | The library shall control Sun Devil Rocketry's one-way telemetry interface by defining the authoritative version in a header for projects to integrate. | mod/_test/mod/nav_isa/results.txt<br>mod/_test/mod/telemetry/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00053 | The library shall provide a method to fuse sensor data. | mod/_test/mod/nav_int/results.txt<br>mod/_test/mod/nav_int/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00054 | The library shall provide a method to initialize the sensor fusion system. | mod/_test/mod/nav_int/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00055 | The library shall call a contract function to prevent concurrent access to its state before accessing state data. | mod/_test/mod/nav_int/results.txt<br>mod/_test/mod/nav_int/results.txt<br>mod/_test/mod/nav_int/results.txt<br>mod/_test/mod/nav_int/results.txt<br>mod/_test/mod/nav_int/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00056 | The library shall invalidate output data that cannot be determined from the configured sources. | mod/_test/mod/nav_int/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00057 | The library shall provide a method to reset velocity integration. | mod/_test/mod/nav_int/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00064 | The library shall provide a valid default configuration. | mod/_test/mod/nav_int/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00036 | The library shall provide a Mahony filter to fuse accelerometer and gyroscope data to return an attitude estimate. | mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00037 | The library shall report vehicle orientation with a unit quaternion. | mod/_test/mod/nav_mahony/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00038 | The project disables fusion. | mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00039 | The provided parameters for accelerometer fusion are invalid. | mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt<br>mod/_test/mod/nav_mahony/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00031 | The library shall provide a method to convert a barometric pressure and temperature reading to an ISA altitude. | mod/_test/mod/nav_isa/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00051 | The library shall provide a method to retrieve a ground reference elevation from current and calibrated pressure and temperature. | mod/_test/mod/nav_isa/results.txt<br>mod/_test/mod/telemetry/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00052 | The library shall provide a method to retrieve the ISA temperature given a barometric pressure reading. | mod/_test/mod/nav_isa/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00058 | The library shall provide a method to set the phase of flight. | mod/_test/mod/nav_int/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00059 | The library shall provide a method to get the phase of flight. | mod/_test/mod/nav_int/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00060 | The library shall update phase of flight during sensor fusion. | mod/_test/mod/nav_pof/results.txt<br>mod/_test/mod/nav_pof/results.txt<br>mod/_test/mod/nav_pof/results.txt<br>mod/_test/mod/nav_pof/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00061 | On-Ground -> Powered Ascent | mod/_test/mod/nav_pof/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00062 | Powered Ascent -> Unpowered Ascent | mod/_test/mod/nav_pof/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |
| RQ.MOD.00063 | Ascent -> Descent | mod/_test/mod/nav_pof/results.txt | <span style="color: #15803d"><strong>PASS</strong></span> |

# 9. FLIGHT QUALIFICATION

The project meets the requirements for flight:

- Test procedures have been applied and have passed their acceptance criteria
- A random sample of test procedures shows that they were performed as specified
- No major design or production revisions have been made since test completion

**Date:** 11/26/2026  
**Project Engineer:** Eli Sells  
**Quality Assurance:** Nicholas Armistead  
