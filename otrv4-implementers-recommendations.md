# OTR version 4 recommendations for client implementers

```
Disclaimer

This protocol specification is a draft. It's currently under constant revision.
```

This document describes some recommendations for client implementers of the
[version 4 of the Off-the-Record Messaging protocol](https://github.com/otrv4/otrv4/blob/master/otrv4.md).
This document expands on what is described in the protocol and implementers
can decide if they follow them or not.

## Table of Contents

1. [Long-term key material advice](#main-changes-over-version-3)
   1. [Exporting/importing long-term keys](#conversation-started-by-an-interactive-dake)
   1. [Verification of long-term keys](#conversation-started-by-an-interactive-dake)
   1. [Forging keys and its private counterpart](#conversation-started-by-an-interactive-dake)
1. [Persistent values advice](#main-changes-over-version-3)
1. [Ephemeral key advice](#main-changes-over-version-3)
   1. [Working with the extra symmetric key](#conversation-started-by-an-interactive-dake)
1. [Double ratchet algorithm advice](#main-changes-over-version-3)
   1. [Defining Phi](#conversation-started-by-an-interactive-dake)
   1. [Test cases](#conversation-started-by-an-interactive-dake)
1. [Handling of data messages advice](#main-changes-over-version-3)
   1. [Handling TLV type 1 Disconnected](#conversation-started-by-an-interactive-dake)
   1. [Conversion of decrypted plaintext](#conversation-started-by-an-interactive-dake)
1. [Protocol state machine advice](#main-changes-over-version-3)
   1. [Handling delayed messages](#conversation-started-by-an-interactive-dake)
   1. [Queueing messages](#conversation-started-by-an-interactive-dake)
   1. [OTRv3 and OTRv4 state machine](#conversation-started-by-an-interactive-dake)
1. [OTRv4 policies advice](#main-changes-over-version-3)
   1. [Defining OTRv4 policies](#conversation-started-by-an-interactive-dake)
   1. [Working with instance tags](#conversation-started-by-an-interactive-dake)
1. [General OTRv4 advice](#main-changes-over-version-3)
   1. [Working with threads](#conversation-started-by-an-interactive-dake)
   1. [Handling chat history](#conversation-started-by-an-interactive-dake)
