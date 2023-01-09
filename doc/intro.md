# Introduction to the Log4j vulnerability

## Overview

The log4j vulnerability is a security flaw that affects the log4j library, which is a popular logging utility used in Java applications. This vulnerability allows attackers to execute arbitrary code on the affected system by injecting malicious payloads into log messages.

The log4j vulnerability is caused by the lack of input validation in the log4j library. When log messages are processed, the log4j library does not properly sanitize the input, allowing attackers to inject malicious payloads into log messages. This can be done through various methods, such as using special characters or exploiting vulnerabilities in log message formatting.

The log4j vulnerability can be exploited to execute malicious code on the affected system, potentially giving attackers access to sensitive information or allowing them to manipulate the system for their own purposes.


## Scenario

![intro](img/log4j-exploit.png)


## Let's get started

We will use this vulnerability to demonstrate how Calico Cloud can be used to prevent, detect, and mitigate the risk of threats that involve containers.


[Next -> Module 4](prevention.md)
